## **Callbacks in TensorFlow/Keras**

**Callbacks** are functions or objects that are called at specific points during training in Keras models. They provide an easy way to track or modify the training process. You can use callbacks for things like monitoring the training process, saving models, stopping training early, or adjusting the learning rate during training.

Below is a detailed note on Keras Callbacks, describing the different types of callbacks and their parameters, followed by example syntax.

---

### **Keras Callback Types**

| **Callback Type**            | **Description**                                                                                     | **Key Parameters**                                                                                        | **Syntax Example**                                                                                       |
|------------------------------|-----------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|
| **ModelCheckpoint**           | Saves the model at intervals during training. Useful for saving the best model during training.    | `filepath (str)`: Path to save model; `monitor (str)`: Metric to monitor; `save_best_only (bool)`: Save only the best model based on the metric. | `ModelCheckpoint(filepath='best_model.h5', monitor='val_loss', save_best_only=True)`                  |
| **EarlyStopping**             | Stops training when a monitored metric stops improving, to avoid overfitting.                       | `monitor (str)`: Metric to monitor; `patience (int)`: Number of epochs with no improvement before stopping. | `EarlyStopping(monitor='val_loss', patience=3)`                                                        |
| **ReduceLROnPlateau**         | Reduces learning rate when a metric has stopped improving.                                         | `monitor (str)`: Metric to monitor; `factor (float)`: Factor to reduce the learning rate; `patience (int)`: Number of epochs with no improvement. | `ReduceLROnPlateau(monitor='val_loss', factor=0.1, patience=2)`                                         |
| **TensorBoard**               | Provides real-time visualizations of metrics during training, such as loss, accuracy, etc.          | `log_dir (str)`: Directory for saving logs; `histogram_freq (int)`: Frequency of histogram computation.    | `TensorBoard(log_dir='logs/', histogram_freq=1)`                                                        |
| **CSVLogger**                 | Streams training metrics to a CSV file during training.                                            | `filename (str)`: File path for saving CSV log file.                                                     | `CSVLogger('training_log.csv')`                                                                          |
| **LambdaCallback**            | Allows you to define custom callbacks using lambda functions.                                        | `on_epoch_end (function)`: Custom function to be called at the end of each epoch; `on_batch_end (function)`: Custom function for each batch. | `LambdaCallback(on_epoch_end=lambda epoch, logs: print(epoch))`                                        |
| **TerminateOnNaN**            | Stops training when a NaN (Not a Number) value is encountered in the loss or other metrics.         | No parameters.                                                                                             | `TerminateOnNaN()`                                                                                       |
| **Progbar**                   | A progress bar callback that shows training progress during epochs. It’s built into TensorFlow.     | No parameters.                                                                                             | `Progbar(target=100)`                                                                                    |
| **BaseCallback**              | A base class for creating custom callbacks. It provides methods like `on_epoch_end`, `on_batch_end` for customization. | No parameters.                                                                                             | Custom subclass of `tf.keras.callbacks.Callback`                                                        |

---

### **Key Callback Parameters and Functions**

Each callback typically contains certain parameters and a set of functions that are triggered at different stages of training. Below is a breakdown of the parameters and functions.

| **Parameter/Function**    | **Description**                                                                                             | **Example/Function Call**                                                                                         |
|---------------------------|-------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------|
| **`on_epoch_end(epoch, logs)`** | Triggered at the end of each epoch, with `epoch` being the current epoch number and `logs` a dictionary of metrics. | `def on_epoch_end(epoch, logs): print(epoch, logs)`                                                                |
| **`on_batch_end(batch, logs)`** | Triggered at the end of each batch, with `batch` being the current batch number and `logs` a dictionary of batch metrics. | `def on_batch_end(batch, logs): print(batch, logs)`                                                                |
| **`monitor`**              | The metric to be monitored for callbacks like `ModelCheckpoint`, `EarlyStopping`, etc.                       | `'val_loss'`, `'accuracy'`, `'val_accuracy'`                                                                       |
| **`patience`**             | Defines how many epochs with no improvement to wait before stopping or reducing the learning rate.          | `patience=5` (for early stopping, will wait 5 epochs with no improvement)                                          |
| **`save_best_only`**       | For `ModelCheckpoint`, saves only the model when the monitored metric is better than before.                | `save_best_only=True`                                                                                              |
| **`restore_best_weights`** | For `EarlyStopping`, restores the weights from the epoch with the best value of the monitored metric.        | `restore_best_weights=True`                                                                                         |
| **`factor`**               | For `ReduceLROnPlateau`, the factor by which the learning rate will be reduced.                             | `factor=0.1` (reduces learning rate by 10% if no improvement is seen)                                              |
| **`log_dir`**              | For `TensorBoard`, specifies the directory where logs will be saved for visualizations.                     | `log_dir='logs/'`                                                                                                  |
| **`histogram_freq`**       | For `TensorBoard`, controls the frequency of histogram computation for weights and activations.             | `histogram_freq=1` (computes histogram once per epoch)                                                             |

---

### **Callback Examples and Usage**

#### **1. ModelCheckpoint** - Saving the Best Model

```python
from tensorflow.keras.callbacks import ModelCheckpoint

checkpoint_callback = ModelCheckpoint(filepath='best_model.h5', monitor='val_loss', save_best_only=True)

model.fit(X_train, y_train, epochs=10, validation_data=(X_val, y_val), callbacks=[checkpoint_callback])
```

- **`filepath`**: Specifies the file path to save the model.
- **`monitor`**: Specifies the metric to monitor (e.g., `val_loss`).
- **`save_best_only`**: Saves the model only when the monitored metric improves.

---

#### **2. EarlyStopping** - Stopping Training Early

```python
from tensorflow.keras.callbacks import EarlyStopping

early_stop_callback = EarlyStopping(monitor='val_loss', patience=3, restore_best_weights=True)

model.fit(X_train, y_train, epochs=10, validation_data=(X_val, y_val), callbacks=[early_stop_callback])
```

- **`patience`**: Stops training after 3 epochs if `val_loss` doesn't improve.
- **`restore_best_weights`**: Restores the weights from the best epoch.

---

#### **3. ReduceLROnPlateau** - Reducing Learning Rate When Metric Stops Improving

```python
from tensorflow.keras.callbacks import ReduceLROnPlateau

reduce_lr_callback = ReduceLROnPlateau(monitor='val_loss', factor=0.1, patience=2)

model.fit(X_train, y_train, epochs=10, validation_data=(X_val, y_val), callbacks=[reduce_lr_callback])
```

- **`factor`**: Reduces the learning rate by 10% when `val_loss` doesn’t improve after 2 epochs.

---

#### **4. TensorBoard** - Logging for Visualization

```python
from tensorflow.keras.callbacks import TensorBoard

tensorboard_callback = TensorBoard(log_dir='logs/', histogram_freq=1)

model.fit(X_train, y_train, epochs=10, validation_data=(X_val, y_val), callbacks=[tensorboard_callback])
```

- **`log_dir`**: Directory where the TensorBoard logs will be stored.
- **`histogram_freq`**: Set to `1` to compute weight histograms once per epoch.

---

#### **5. LambdaCallback** - Custom Callback

```python
from tensorflow.keras.callbacks import LambdaCallback

lambda_callback = LambdaCallback(on_epoch_end=lambda epoch, logs: print(f'Epoch {epoch}: {logs}'))

model.fit(X_train, y_train, epochs=10, validation_data=(X_val, y_val), callbacks=[lambda_callback])
```

- **`on_epoch_end`**: Custom function that gets called after each epoch to print logs.

---

### **Summary Table of Common Callbacks**

| **Callback Type**            | **Key Parameters**                                                                                              | **Purpose**                                                                         | **Example Syntax**                                                                                  |
|------------------------------|------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|
| **ModelCheckpoint**           | `monitor`, `save_best_only`, `filepath`                                                                         | Saves the best model during training based on monitored metric.                      | `ModelCheckpoint(filepath='best_model.h5', monitor='val_loss', save_best_only=True)`              |
| **EarlyStopping**             | `monitor`, `patience`, `restore_best_weights`                                                                    | Stops training early if monitored metric stops improving.                           | `EarlyStopping(monitor='val_loss', patience=3, restore_best_weights=True)`                        |
| **ReduceLROnPlateau**         | `monitor`, `factor`, `patience`, `min_lr`                                                                         | Reduces learning rate when a metric plateaus.                                       | `ReduceLROnPlateau(monitor='val_loss', factor=0.1, patience=2)`                                    |
| **TensorBoard**               | `log_dir`, `histogram_freq`, `write_graph`, `write_images`                                                        | Logs data for visualization in TensorBoard.                                         | `TensorBoard(log_dir='logs/', histogram_freq=1)`                                                   |
| **CSVLogger**                 | `filename`                                                                                                       | Logs training metrics to a CSV file.                                                | `CSVLogger('training_log.csv')`                                                                   |
| **LambdaCallback**            | `on_epoch_end`, `on_batch_end`                                                                                   | Custom callback with user-defined behavior.                                          | `LambdaCallback(on_epoch_end=lambda epoch, logs: print(epoch, logs))`                             |
| **TerminateOnNaN**            | No parameters                                                                                                    | Terminates training when a NaN is encountered in the loss or metrics.               | `TerminateOnNaN()`                                                                                 |
| **Progbar**                   | `target`, `verbose`                                                                                              | Displays a progress bar during training.                                            | `Progbar(target=100)`                                                                              |

---

### **Conclusion**

Callbacks in TensorFlow/Keras provide a powerful and flexible way to control and monitor the training process. The above table and examples should help you effectively utilize callbacks like `ModelCheckpoint`, `EarlyStopping`, `ReduceLROnPlateau`, and more.