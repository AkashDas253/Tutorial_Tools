# Metrics (`tf.keras.metrics`)

---

## What Are Metrics?

**Metrics** are functions used to **evaluate the performance** of a machine learning model during training, validation, and testing.
They do **not affect the training** (unlike loss), but help monitor and compare models.

---

## How to Use

### In Model Compilation

```python
model.compile(
    optimizer='adam',
    loss='sparse_categorical_crossentropy',
    metrics=['accuracy']
)
```

### As Classes

```python
metric = tf.keras.metrics.Accuracy()
metric.update_state(y_true, y_pred)
result = metric.result()
```

---

## Built-in Metric Categories

---

### 1. **Classification Metrics**

| Metric                         | Description                                       |
| ------------------------------ | ------------------------------------------------- |
| `Accuracy`                     | Fraction of correct predictions                   |
| `BinaryAccuracy`               | Accuracy for binary classification                |
| `CategoricalAccuracy`          | Accuracy for one-hot encoded targets              |
| `SparseCategoricalAccuracy`    | Accuracy for integer encoded targets              |
| `TopKCategoricalAccuracy(k=n)` | Accuracy where true label is in top-n predictions |
| `AUC`                          | Area under ROC curve (for binary classification)  |
| `Precision`                    | True positives / (TP + FP)                        |
| `Recall`                       | True positives / (TP + FN)                        |
| `F1Score` (via `tf-addons`)    | Harmonic mean of precision and recall             |

---

### 2. **Regression Metrics**

| Metric                        | Description                              |
| ----------------------------- | ---------------------------------------- |
| `MeanAbsoluteError`           | Average absolute error                   |
| `MeanSquaredError`            | Average squared error                    |
| `MeanAbsolutePercentageError` | Relative percentage error                |
| `RootMeanSquaredError`        | Square root of MSE                       |
| `CosineSimilarity`            | Direction similarity between vectors     |
| `MeanSquaredLogarithmicError` | Penalizes underestimation more than over |

---

### 3. **Probabilistic Metrics**

| Metric         | Description                                      |
| -------------- | ------------------------------------------------ |
| `KLDivergence` | Divergence between two probability distributions |

---

## Key Arguments

| Argument      | Description                                     |
| ------------- | ----------------------------------------------- |
| `name`        | Name of the metric                              |
| `dtype`       | Output data type (e.g., `tf.float32`)           |
| `thresholds`  | For metrics like precision/recall               |
| `top_k`       | For top-k accuracy calculations                 |
| `from_logits` | Whether predictions are raw logits              |
| `multi_label` | For multilabel classification tasks (e.g., AUC) |

---

## Using Custom Metrics

### Function-based

```python
def f1_score(y_true, y_pred):
    precision = ...
    recall = ...
    return 2 * ((precision * recall) / (precision + recall + 1e-7))
```

### Class-based

```python
class CustomAccuracy(tf.keras.metrics.Metric):
    def __init__(self, name="custom_accuracy", **kwargs):
        super().__init__(name=name, **kwargs)
        self.total = self.add_weight(name="total", initializer="zeros")
        self.count = self.add_weight(name="count", initializer="zeros")

    def update_state(self, y_true, y_pred, sample_weight=None):
        values = tf.equal(tf.argmax(y_true, axis=1), tf.argmax(y_pred, axis=1))
        self.total.assign_add(tf.reduce_sum(tf.cast(values, tf.float32)))
        self.count.assign_add(tf.cast(tf.size(y_true[:, 0]), tf.float32))

    def result(self):
        return self.total / self.count
```

---

## Monitoring During Training

* The `fit()` function tracks and displays metric values over epochs.
* Can be visualized with:

  * `history.history` object
  * `TensorBoard` metrics

---

## Summary Table

| Task                      | Recommended Metric(s)                                           |
| ------------------------- | --------------------------------------------------------------- |
| Binary classification     | `BinaryAccuracy`, `AUC`, `Precision`, `Recall`                  |
| Multiclass classification | `SparseCategoricalAccuracy`, `TopKCategoricalAccuracy`          |
| Regression                | `MeanAbsoluteError`, `MeanSquaredError`, `RootMeanSquaredError` |
| Probabilistic models      | `KLDivergence`, `CosineSimilarity`                              |
| Custom metrics            | Use `Metric` subclass or function                               |

---
