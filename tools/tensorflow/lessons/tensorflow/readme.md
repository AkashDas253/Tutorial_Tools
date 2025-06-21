# Overview of TensorFlow

---

## What is TensorFlow?

TensorFlow is an **open-source machine learning framework** developed by **Google Brain Team** for building and training ML models, especially deep learning models. It uses **dataflow graphs** to represent computations, allowing deployment across CPUs, GPUs, TPUs, and mobile devices.

---

## Core Components

| Component       | Description                                                           |
| --------------- | --------------------------------------------------------------------- |
| `tf.Tensor`     | Core data structure; n-dimensional array with uniform type            |
| `tf.Variable`   | Mutable tensor used to store parameters                               |
| `tf.Graph`      | Representation of computations as a dataflow graph (in low-level API) |
| `tf.Session`    | (TF 1.x) Executes operations in a Graph (Deprecated in TF 2.x)        |
| `tf.function`   | Converts Python code into a TensorFlow graph in TF 2.x                |
| `Keras`         | High-level API for building and training models                       |
| `Estimator` API | High-level API (mostly for production and distributed training)       |
| `TensorBoard`   | Visualization tool for debugging, profiling, and tracking training    |
| `SavedModel`    | Universal format for saving TF models                                 |
| `TF Lite`       | Lightweight version of TensorFlow for mobile/embedded devices         |
| `TF Serving`    | Serving models in production environments                             |
| `TF Hub`        | Repository of reusable pre-trained models                             |

---

## Architecture

```mermaid
flowchart TD;
    A[Client Program (Python)] --> B[TensorFlow API];
    B --> C[TensorFlow Core (C++)];
    C --> D[Executor];
    D --> E[Hardware Abstraction Layer];
    E --> F[CPU/GPU/TPU];
```

* **Frontend (Python API)**: Developer-facing interface
* **Backend (C++)**: Manages actual computation and execution
* **Executor**: Converts graphs into executable operations
* **Device Layer**: Assigns operations to hardware

---

## Execution Modes

* **Eager Execution (Default in TF 2.x)**: Operations run immediately (imperative)
* **Graph Execution**: Compiles into static computation graph using `@tf.function`

---

## TensorFlow vs Keras

| Feature     | TensorFlow Core | Keras (within TensorFlow)    |
| ----------- | --------------- | ---------------------------- |
| Level       | Low-level       | High-level                   |
| Flexibility | Very high       | Easier to use, less flexible |
| API         | Procedural      | Object-oriented              |

---

## Data Handling

* **`tf.data` API**: Efficient input pipeline construction

  * `Dataset.from_tensor_slices()`
  * `Dataset.map()`, `batch()`, `shuffle()`, `prefetch()`
* **Feature Columns**: Abstractions for structured data input
* **`tf.io`**: Low-level utilities for I/O operations

---

## Model Building Approaches

* **Sequential API**: `tf.keras.Sequential([...])`
* **Functional API**: `tf.keras.Model(inputs, outputs)`
* **Subclassing API**: Custom models using OOP inheritance

---

## Layers API (`tf.keras.layers`)

| Layer Type    | Examples                               |
| ------------- | -------------------------------------- |
| Core Layers   | Dense, Dropout, Flatten                |
| Convolutional | Conv1D, Conv2D, Conv3D                 |
| Recurrent     | LSTM, GRU, SimpleRNN                   |
| Normalization | BatchNormalization, LayerNormalization |
| Pooling       | MaxPooling2D, AveragePooling2D         |
| Embedding     | Embedding                              |
| Attention     | MultiHeadAttention, Attention          |

---

## Training

* **Compile**: `model.compile(optimizer, loss, metrics)`
* **Train**: `model.fit(dataset, epochs, callbacks)`
* **Evaluate**: `model.evaluate()`
* **Predict**: `model.predict()`

---

## Optimizers (`tf.keras.optimizers`)

| Optimizer | Description                 |
| --------- | --------------------------- |
| SGD       | Stochastic Gradient Descent |
| Adam      | Adaptive learning rate      |
| RMSprop   | Gradient normalization      |
| Adagrad   | Per-parameter learning rate |

---

## Loss Functions (`tf.keras.losses`)

| Type           | Examples                                              |
| -------------- | ----------------------------------------------------- |
| Regression     | `MSE`, `MAE`, `Huber`                                 |
| Classification | `SparseCategoricalCrossentropy`, `BinaryCrossentropy` |

---

## Metrics (`tf.keras.metrics`)

* Accuracy, Precision, Recall, AUC, etc.
* Custom metrics can be defined using functions or subclassing `tf.keras.metrics.Metric`

---

## Callbacks (`tf.keras.callbacks`)

| Callback            | Purpose                          |
| ------------------- | -------------------------------- |
| `ModelCheckpoint`   | Save model during/after training |
| `EarlyStopping`     | Stop training early on plateau   |
| `TensorBoard`       | Log data for visualization       |
| `ReduceLROnPlateau` | Reduce LR on stagnation          |

---

## Distributed Training

* `tf.distribute.Strategy`

  * `MirroredStrategy`: Multi-GPU on single machine
  * `MultiWorkerMirroredStrategy`: Multi-machine
  * `TPUStrategy`: TPU training

---

## Model Deployment

| Option       | Description                            |
| ------------ | -------------------------------------- |
| `SavedModel` | Portable format for deployment         |
| `TF Serving` | Server for REST/gRPC deployment        |
| `TF Lite`    | Deploy to mobile/IoT                   |
| `TF.js`      | Run models in browsers with JavaScript |

---

## Model Serialization

* Save: `model.save('path')`
* Load: `tf.keras.models.load_model('path')`

Formats:

* HDF5 (`.h5`)
* SavedModel (directory)

---

## TensorFlow Ecosystem

| Tool          | Purpose                      |
| ------------- | ---------------------------- |
| `TensorBoard` | Visualization & Debugging    |
| `TF Lite`     | Mobile/Embedded deployment   |
| `TF.js`       | Web deployment               |
| `TFX`         | Production ML pipelines      |
| `TF Hub`      | Pretrained model sharing     |
| `TF Datasets` | Preprocessed public datasets |

---

## Transfer Learning

* Load base model (`include_top=False`)
* Add new head layers
* Freeze layers optionally
* Fine-tune with small learning rate

---

## Quantization, Pruning, and Optimization

* **Quantization**: Convert weights to int8/float16 for smaller model
* **Pruning**: Remove insignificant weights
* **Clustering**: Group similar weights
* Used during **model compression** and **deployment optimization**

---

## Common Use Cases

* Image Classification
* Object Detection
* NLP Tasks (e.g., BERT, LSTM)
* Time Series Forecasting
* GANs and Autoencoders
* Recommendation Systems

---
