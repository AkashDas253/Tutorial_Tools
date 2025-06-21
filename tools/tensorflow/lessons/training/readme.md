# Training (Using `tf.keras`)

---

## Overview

Model training in TensorFlow is handled primarily via the `tf.keras.Model` API using:

* High-level methods like `compile()`, `fit()`, `evaluate()`, `predict()`
* Custom training loops for advanced use cases (using `GradientTape`)

---

## 1. Model Compilation

Before training, models must be **compiled** with:

| Component | Purpose                               |
| --------- | ------------------------------------- |
| Optimizer | Update weights to minimize loss       |
| Loss      | Measure prediction error              |
| Metrics   | Evaluate performance (e.g., accuracy) |

### Syntax

```python
model.compile(
    optimizer='adam',
    loss='sparse_categorical_crossentropy',
    metrics=['accuracy']
)
```

---

## 2. Model Training with `fit()`

### Syntax

```python
history = model.fit(
    x_train, y_train,
    epochs=10,
    batch_size=32,
    validation_data=(x_val, y_val),
    callbacks=[...]
)
```

### Key Arguments

| Argument          | Description                                         |
| ----------------- | --------------------------------------------------- |
| `x`, `y`          | Input and target data                               |
| `batch_size`      | Size of batches fed into model                      |
| `epochs`          | Number of full passes through the dataset           |
| `validation_data` | Data for validation during training                 |
| `callbacks`       | List of `tf.keras.callbacks` for monitoring control |

---

## 3. Model Evaluation

```python
model.evaluate(x_test, y_test)
```

Returns loss and metric values on the test dataset.

---

## 4. Model Prediction

```python
predictions = model.predict(x_input)
```

Outputs raw predictions (e.g., logits or probabilities).

---

## 5. Training with `tf.data.Dataset`

For large or preprocessed data:

```python
model.fit(train_dataset, epochs=10, validation_data=val_dataset)
```

* Use batching, shuffling, and prefetching for performance.
* Supports infinite streaming datasets with `.repeat()`

---

## 6. Callbacks for Training Control

| Callback                | Purpose                           |
| ----------------------- | --------------------------------- |
| `ModelCheckpoint`       | Save best model during training   |
| `EarlyStopping`         | Stop training when no improvement |
| `TensorBoard`           | Log metrics for visualization     |
| `ReduceLROnPlateau`     | Lower LR when metric plateaus     |
| `LearningRateScheduler` | Dynamic LR adjustment             |

### Example

```python
callbacks = [
    tf.keras.callbacks.EarlyStopping(patience=3),
    tf.keras.callbacks.ModelCheckpoint('best_model.h5', save_best_only=True)
]
```

---

## 7. Custom Training Loop (Advanced)

Use `tf.GradientTape` for full control.

### Example

```python
for epoch in range(num_epochs):
    for x_batch, y_batch in train_dataset:
        with tf.GradientTape() as tape:
            y_pred = model(x_batch, training=True)
            loss = loss_fn(y_batch, y_pred)
        grads = tape.gradient(loss, model.trainable_variables)
        optimizer.apply_gradients(zip(grads, model.trainable_variables))
```

---

## 8. Training with Multiple GPUs / Devices

Use `tf.distribute.Strategy` for scaling:

```python
strategy = tf.distribute.MirroredStrategy()
with strategy.scope():
    model = create_model()
    model.compile(...)
```

Supports:

* `MirroredStrategy`: Multi-GPU
* `TPUStrategy`: TPU-based training
* `MultiWorkerMirroredStrategy`: Multi-machine

---

## 9. Performance Tips

| Tip                             | Benefit                                  |
| ------------------------------- | ---------------------------------------- |
| Use `prefetch`, `cache`         | Efficient data pipeline                  |
| Use `AUTOTUNE` buffer sizes     | Adaptive performance tuning              |
| Mixed precision training        | Faster training with less memory usage   |
| Enable XLA (`jit_compile=True`) | Accelerated kernel fusion & optimization |

---

## 10. Monitoring Training

Use:

* `history.history`: Access training logs (loss, accuracy)
* `TensorBoard`: For visual monitoring

```python
%tensorboard --logdir logs/
```

---

## Summary

| Step        | API / Method                   |
| ----------- | ------------------------------ |
| Compile     | `model.compile()`              |
| Train       | `model.fit()`                  |
| Evaluate    | `model.evaluate()`             |
| Predict     | `model.predict()`              |
| Custom Loop | `tf.GradientTape()`            |
| Distributed | `tf.distribute.Strategy`       |
| Monitoring  | Callbacks, `TensorBoard`, logs |

---
