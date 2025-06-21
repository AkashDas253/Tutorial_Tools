# **how-to list for TensorFlow**

## Basic / Fundamental

* **Install TensorFlow**
  Install via pip: `pip install tensorflow`

* **Create and Manipulate Tensors**
  Use `tf.constant`, `tf.Variable`, and basic tensor operations like addition, multiplication, reshaping, slicing.

* **Perform Basic Math Operations**
  Use `tf.math` functions such as `tf.math.add`, `tf.math.reduce_mean`, `tf.linalg.matmul`.

* **Use Eager Execution**
  Default in TensorFlow 2.x; operations run immediately without building graphs.

* **Load and Convert Data**
  Convert NumPy arrays and Pandas DataFrames into tensors using `tf.convert_to_tensor`.

* **Build and Train Sequential Model**
  Use `tf.keras.Sequential` with `.compile()`, `.fit()`, `.evaluate()`, `.predict()`.

* **Use Built-in Datasets**
  Load with `tf.keras.datasets`, e.g., `mnist`, `cifar10`.

---

## Intermediate

* **Build Models Using Functional API**
  Create complex models with multiple inputs and outputs using `tf.keras.Model`.

* **Customize Data Pipelines with `tf.data`**
  Use `tf.data.Dataset.from_tensor_slices()`, `shuffle()`, `batch()`, `map()`, `prefetch()`.

* **Apply Callbacks**
  Use `tf.keras.callbacks` like `EarlyStopping`, `ModelCheckpoint`, `TensorBoard`, and `ReduceLROnPlateau`.

* **Use TensorBoard for Visualization**
  Track training metrics, weights, graphs, and histograms.

* **Perform Transfer Learning**
  Load a pretrained model (`include_top=False`), freeze layers, and add new trainable layers.

* **Define Custom Losses and Metrics**
  Create by subclassing `tf.keras.losses.Loss` or `tf.keras.metrics.Metric`.

* **Use Model Subclassing API**
  Define a custom model class inheriting from `tf.keras.Model`, override `__init__` and `call`.

* **Convert Functions to Graphs**
  Use `@tf.function` decorator to create graph-executable functions.

* **Work with Feature Columns**
  Transform structured data using `tf.feature_column`.

---

## Advanced

* **Implement Custom Training Loops with `tf.GradientTape`**
  Full control over forward and backward pass, loss computation, and optimization steps.

* **Use `tf.distribute.Strategy` for Distributed Training**
  Distribute training on multiple GPUs or TPUs using `MirroredStrategy`, `MultiWorkerMirroredStrategy`, `TPUStrategy`.

* **Optimize Models for Deployment**
  Apply model pruning, quantization, weight clustering using `tensorflow_model_optimization`.

* **Export Models using SavedModel or HDF5**
  Save models via `model.save()` and load via `tf.keras.models.load_model()`.

* **Serve Models with TensorFlow Serving**
  Deploy models using REST or gRPC endpoints.

* **Deploy Models with TensorFlow Lite**
  Convert models with `TFLiteConverter` for mobile or edge devices.

* **Build and Train Generative Models**
  Implement GANs, VAEs, and other advanced architectures.

* **Work with Time Series and Sequence Models**
  Use RNNs, GRUs, LSTMs, and Transformer-based models.

* **Create and Use Custom Layers**
  Inherit from `tf.keras.layers.Layer`, define custom computation logic in `call`.

* **Build Production Pipelines with TFX**
  Use TensorFlow Extended to build end-to-end ML pipelines for production.

---
