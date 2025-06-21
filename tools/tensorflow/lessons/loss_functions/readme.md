# Loss Functions (`tf.keras.losses`)

---

## What Is a Loss Function?

A **loss function** measures the difference between the predicted outputs and actual target values.
It guides the **optimization process** by quantifying how well the model is performing.

---

## Usage in Training

```python
model.compile(
    optimizer='adam',
    loss='sparse_categorical_crossentropy',
    metrics=['accuracy']
)
```

You can also use classes directly:

```python
loss_fn = tf.keras.losses.MeanSquaredError()
loss = loss_fn(y_true, y_pred)
```

---

## Categories of Loss Functions

---

### 1. **Regression Losses**

| Loss Function                 | Description                                                |                                     |    |
| ----------------------------- | ---------------------------------------------------------- | ----------------------------------- | -- |
| `MeanSquaredError`            | \$\frac{1}{n}\sum(y\_{\text{true}} - y\_{\text{pred}})^2\$ |                                     |    |
| `MeanAbsoluteError`           | \$\frac{1}{n}\sum                                          | y\_{\text{true}} - y\_{\text{pred}} | \$ |
| `MeanAbsolutePercentageError` | Relative error (MAPE)                                      |                                     |    |
| `MeanSquaredLogarithmicError` | Sensitive to underestimations                              |                                     |    |
| `Huber`                       | Combines MSE and MAE (robust to outliers)                  |                                     |    |
| `LogCosh`                     | Log of cosh, smooth and robust                             |                                     |    |
| `CosineSimilarity`            | Measures similarity in direction (not magnitude)           |                                     |    |

---

### 2. **Binary Classification Losses**

| Loss Function        | Description                           |
| -------------------- | ------------------------------------- |
| `BinaryCrossentropy` | For binary classification (2 classes) |
| `Hinge`              | For SVM-style classifiers             |
| `SquaredHinge`       | Squared version of hinge loss         |

---

### 3. **Multiclass Classification Losses**

| Loss Function                   | Description                               |
| ------------------------------- | ----------------------------------------- |
| `CategoricalCrossentropy`       | Requires one-hot encoded labels           |
| `SparseCategoricalCrossentropy` | Works with integer-encoded labels         |
| `KLDivergence`                  | Measures divergence between distributions |

---

### 4. **Custom Loss Functions**

You can define a custom loss as a function:

```python
def custom_mse(y_true, y_pred):
    return tf.reduce_mean(tf.square(y_true - y_pred))
```

Or by subclassing:

```python
class CustomLoss(tf.keras.losses.Loss):
    def call(self, y_true, y_pred):
        return tf.reduce_mean(tf.square(y_true - y_pred))
```

---

## Function vs Class

| Type           | Syntax Example                            |
| -------------- | ----------------------------------------- |
| Function-based | `loss='mean_squared_error'`               |
| Class-based    | `loss=tf.keras.losses.MeanSquaredError()` |

---

## Important Parameters

| Parameter     | Description                                                            | Default               |
| ------------- | ---------------------------------------------------------------------- | --------------------- |
| `from_logits` | Set `True` if predictions are not passed through softmax or sigmoid    | `False`               |
| `reduction`   | Controls loss reduction (`auto`, `sum`, `none`, `sum_over_batch_size`) | `SUM_OVER_BATCH_SIZE` |

---

## Choosing the Right Loss

| Problem Type                        | Recommended Loss                                                                        |
| ----------------------------------- | --------------------------------------------------------------------------------------- |
| Binary classification               | `BinaryCrossentropy`                                                                    |
| Multiclass classification           | `SparseCategoricalCrossentropy` (integer labels)<br>`CategoricalCrossentropy` (one-hot) |
| Regression (small errors)           | `MeanSquaredError`                                                                      |
| Regression (robust to outliers)     | `Huber`                                                                                 |
| Probability distribution comparison | `KLDivergence`                                                                          |
| SVM-like binary classification      | `Hinge`, `SquaredHinge`                                                                 |
| Cosine similarity matching          | `CosineSimilarity`                                                                      |

---

## Summary Table

| Name                            | API Name                                     | Use Case                    |
| ------------------------------- | -------------------------------------------- | --------------------------- |
| Mean Squared Error              | `MeanSquaredError()`                         | Regression                  |
| Mean Absolute Error             | `MeanAbsoluteError()`                        | Regression                  |
| Huber Loss                      | `Huber(delta=1.0)`                           | Regression with outliers    |
| Log Cosh                        | `LogCosh()`                                  | Regression, smooth loss     |
| Binary Crossentropy             | `BinaryCrossentropy(from_logits=False)`      | Binary classification       |
| Categorical Crossentropy        | `CategoricalCrossentropy(from_logits=False)` | Multiclass (one-hot)        |
| Sparse Categorical Crossentropy | `SparseCategoricalCrossentropy()`            | Multiclass (integer labels) |
| Cosine Similarity               | `CosineSimilarity(axis=-1)`                  | Direction similarity        |
| Kullback-Leibler Divergence     | `KLDivergence()`                             | Distribution comparison     |

---
