# Core Components

---

## Tensor

* Fundamental unit of data in TensorFlow.
* Represents an n-dimensional array.
* Types:

  * Scalar (0D)
  * Vector (1D)
  * Matrix (2D)
  * Higher-Dimensional tensors (3D+)
* Created using `tf.constant`, `tf.Variable`, `tf.convert_to_tensor`, or as outputs from operations.

---

## Variable

* A special type of tensor whose value can be modified during training.
* Used to represent weights and biases in models.
* Syntax:

  ```python
  v = tf.Variable(initial_value)
  ```

---

## Graph

* A computation graph that defines the operations to perform.
* Each node is an operation; edges are tensors.
* TensorFlow 2.x uses eager execution by default, but graphs can be created using `@tf.function`.

---

## Session (TensorFlow 1.x)

* Encapsulates the environment in which Operation objects are executed.
* Used in TensorFlow 1.x to execute graphs.
* Deprecated in TensorFlow 2.x due to eager execution.

---

## Eager Execution

* Default in TensorFlow 2.x.
* Operations are executed immediately and return concrete values.
* Easier to debug, more Pythonic.

---

## tf.function

* Converts Python functions into a callable TensorFlow graph.
* Enables performance optimizations and deployment.
* Syntax:

  ```python
  @tf.function
  def f(x):
      return x * x
  ```

---

## Layers API (`tf.keras.layers`)

* Building blocks for neural networks.
* Common layer types:

  * Core: `Dense`, `Dropout`, `Flatten`
  * Convolutional: `Conv2D`, `Conv1D`
  * Recurrent: `LSTM`, `GRU`
  * Pooling: `MaxPooling2D`, `AveragePooling2D`
  * Normalization: `BatchNormalization`, `LayerNormalization`

---

## Model API (`tf.keras.Model`)

* Base class for all models in Keras.
* Three model types:

  * Sequential API
  * Functional API
  * Model Subclassing

---

## Optimizers (`tf.keras.optimizers`)

* Used to minimize loss functions during training.
* Examples:

  * `SGD`
  * `Adam`
  * `RMSprop`
  * `Adagrad`

---

## Loss Functions (`tf.keras.losses`)

* Measure model prediction error.
* Common losses:

  * `BinaryCrossentropy`
  * `CategoricalCrossentropy`
  * `MeanSquaredError`
  * `Huber`

---

## Metrics (`tf.keras.metrics`)

* Used to monitor training and evaluation.
* Examples:

  * `Accuracy`
  * `Precision`
  * `Recall`
  * `AUC`

---

## tf.data API

* Efficient input pipeline creation.
* Operations:

  * `map`
  * `shuffle`
  * `batch`
  * `repeat`
  * `prefetch`
* Allows lazy and efficient data loading.

---

## Callbacks (`tf.keras.callbacks`)

* Used to customize and control training.
* Common callbacks:

  * `ModelCheckpoint`
  * `EarlyStopping`
  * `ReduceLROnPlateau`
  * `TensorBoard`

---

## TensorBoard

* Visualization toolkit for training logs.
* Monitors:

  * Scalars (loss/accuracy)
  * Graphs
  * Histograms
  * Images

---

## tf.distribute.Strategy

* For distributed training across devices or machines.
* Examples:

  * `MirroredStrategy`: Multi-GPU on single machine
  * `TPUStrategy`: TPU training
  * `MultiWorkerMirroredStrategy`: Multi-host GPU training

---

## SavedModel

* Standard format for saving and deploying models.
* Includes:

  * Model architecture
  * Weights
  * Training configuration
  * Optimizer state

---

## TensorFlow Hub

* Repository for reusable pretrained models.
* Use:

  ```python
  import tensorflow_hub as hub
  model = hub.KerasLayer("model_url")
  ```

---

## TensorFlow Lite

* Framework for deploying models to mobile and embedded devices.
* Supports model quantization and optimization.

---

## TensorFlow Serving

* Tool for deploying TensorFlow models in production.
* Exposes REST/gRPC APIs for prediction serving.

---

## Estimators (Legacy High-level API)

* Encapsulation of training, evaluation, prediction.
* Preconfigured for standard tasks.
* Useful in production pipelines and distributed settings.

---
