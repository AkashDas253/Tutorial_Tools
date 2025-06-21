# Callbacks (`tf.keras.callbacks`)

---

## What Are Callbacks?

**Callbacks** are customizable hooks that allow you to **intervene during training**, validation, and evaluation at key stages like:

* At epoch or batch start/end
* Before or after training
* On plateau or metric changes
* For logging, saving, early stopping, etc.

They’re passed to `model.fit()` using the `callbacks` argument.

---

## Common Use Cases

| Use Case                      | Callback                                     |
| ----------------------------- | -------------------------------------------- |
| Save best model               | `ModelCheckpoint`                            |
| Stop early if no improvement  | `EarlyStopping`                              |
| Adjust learning rate          | `ReduceLROnPlateau`, `LearningRateScheduler` |
| Log metrics for visualization | `TensorBoard`                                |
| Custom training logic         | `LambdaCallback`, custom subclass            |

---

## Built-in Callbacks

### 1. `ModelCheckpoint`

Saves model weights during training.

```python
tf.keras.callbacks.ModelCheckpoint(
    filepath='model.h5',
    save_best_only=True,
    monitor='val_loss',
    mode='min'
)
```

### 2. `EarlyStopping`

Stops training when monitored metric stops improving.

```python
tf.keras.callbacks.EarlyStopping(
    monitor='val_loss',
    patience=3,
    restore_best_weights=True
)
```

### 3. `ReduceLROnPlateau`

Reduces LR when a metric has stopped improving.

```python
tf.keras.callbacks.ReduceLROnPlateau(
    monitor='val_loss',
    factor=0.1,
    patience=2
)
```

### 4. `LearningRateScheduler`

Applies a custom LR schedule each epoch.

```python
def scheduler(epoch, lr):
    return lr * 0.9

tf.keras.callbacks.LearningRateScheduler(scheduler)
```

### 5. `TensorBoard`

Logs training process for TensorBoard visualization.

```python
tf.keras.callbacks.TensorBoard(log_dir='./logs')
```

### 6. `CSVLogger`

Logs training metrics to a CSV file.

```python
tf.keras.callbacks.CSVLogger('training_log.csv')
```

### 7. `TerminateOnNaN`

Stops training if loss becomes NaN.

```python
tf.keras.callbacks.TerminateOnNaN()
```

### 8. `ProgbarLogger`

Displays a progress bar (used internally; rarely overridden).

---

## LambdaCallback: Quick Custom Callback

```python
tf.keras.callbacks.LambdaCallback(
    on_epoch_end=lambda epoch, logs: print(f"Epoch {epoch} ended with loss {logs['loss']}")
)
```

---

## Creating a Custom Callback (Subclassing)

```python
class CustomLogger(tf.keras.callbacks.Callback):
    def on_epoch_end(self, epoch, logs=None):
        print(f"> Epoch {epoch+1} - Accuracy: {logs['accuracy']:.4f}")
```

---

## Integration with `fit()`

```python
model.fit(
    x_train, y_train,
    validation_data=(x_val, y_val),
    epochs=20,
    callbacks=[
        ModelCheckpoint(...),
        EarlyStopping(...),
        TensorBoard(...),
        ReduceLROnPlateau(...)
    ]
)
```

---

## Summary Table

| Callback                | Purpose                          |
| ----------------------- | -------------------------------- |
| `ModelCheckpoint`       | Save model periodically          |
| `EarlyStopping`         | Stop when performance plateaus   |
| `ReduceLROnPlateau`     | Lower LR automatically           |
| `LearningRateScheduler` | Custom LR adjustments            |
| `TensorBoard`           | Visualize logs                   |
| `CSVLogger`             | Save training history            |
| `TerminateOnNaN`        | Halt if NaN encountered          |
| `LambdaCallback`        | Simple inline custom logic       |
| `CustomCallback`        | Fully control training behaviors |

---
