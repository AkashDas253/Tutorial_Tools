## Keras: Core Concepts and Subconcepts

- **High-Level API**
  - Sequential API
    - Adding layers sequentially
    - Simple model definition
  - Functional API
    - Complex architectures
    - Models with multiple inputs/outputs
  - Model Subclassing
    - Custom model creation
    - Extending `tf.keras.Model`

---

- **Layers**
  - Core Layers
    - `Dense`, `Flatten`, `Input`, `Reshape`
  - Convolutional Layers
    - `Conv2D`, `Conv3D`, `Conv1D`
    - `SeparableConv2D`, `Conv2DTranspose`
  - Pooling Layers
    - `MaxPooling2D`, `AveragePooling2D`
    - `GlobalMaxPooling2D`, `GlobalAveragePooling2D`
  - Recurrent Layers
    - `SimpleRNN`, `LSTM`, `GRU`
    - Bidirectional, TimeDistributed
  - Normalization Layers
    - `BatchNormalization`, `LayerNormalization`
  - Activation Layers
    - `ReLU`, `Softmax`, `Sigmoid`
    - Custom activation functions
  - Regularization Layers
    - `Dropout`, `SpatialDropout2D`
    - `AlphaDropout`, `GaussianDropout`
  - Embedding Layers
    - `Embedding`
  - Attention Layers
    - `AdditiveAttention`, `MultiHeadAttention`
  - Other Specialized Layers
    - `Lambda`, `Cropping2D`, `Masking`

---

- **Loss Functions**
  - Predefined Losses
    - Regression: `MeanSquaredError`, `MeanAbsoluteError`
    - Classification: `BinaryCrossentropy`, `CategoricalCrossentropy`
    - Custom Loss Functions
  - Weighted Loss Functions

---

- **Metrics**
  - Accuracy
    - `Accuracy`, `BinaryAccuracy`, `CategoricalAccuracy`
  - Precision, Recall, F1-Score
  - Custom Metrics

---

- **Optimizers**
  - Gradient-Based Optimizers
    - `SGD`, `Adam`, `RMSprop`, `Adagrad`
    - Learning Rate Schedules
  - Adaptive Optimizers
    - `AdamW`, `Nadam`, `AdaDelta`

---

- **Callbacks**
  - Common Callbacks
    - `ModelCheckpoint`, `EarlyStopping`, `ReduceLROnPlateau`
    - `TensorBoard`, `CSVLogger`
  - Custom Callbacks

---

- **Model Training**
  - Training Functions
    - `model.fit`, `model.evaluate`, `model.predict`
  - Dataset Handling
    - `tf.data.Dataset`, Data augmentation
  - Model Validation
    - Validation splits, K-Fold cross-validation

---

- **Model Evaluation**
  - Performance Metrics
    - Loss and accuracy trends
  - Hyperparameter tuning

---

- **Model Saving and Serialization**
  - Saving Models
    - Entire model: `.h5`, `SavedModel` format
    - Weights only
  - Loading Models
    - `load_model`, `load_weights`

---

- **Transfer Learning**
  - Pretrained Models
    - `VGG16`, `ResNet`, `MobileNet`, etc.
  - Fine-tuning Pretrained Models

---

- **Custom Layers and Models**
  - Creating Custom Layers
    - Inheriting from `tf.keras.layers.Layer`
  - Defining Custom Models
    - Inheriting from `tf.keras.Model`

---

- **Distributed Training**
  - Multi-GPU Training
  - TPU Training
  - Strategy API
    - `MirroredStrategy`, `TPUStrategy`

---

- **Data Preprocessing**
  - Image Preprocessing
    - `ImageDataGenerator`, `image_dataset_from_directory`
  - Text Preprocessing
    - Tokenization, padding
  - Sequence Data
    - `TimeseriesGenerator`

---

- **Visualization**
  - Training Visualization
    - TensorBoard, Matplotlib plots
  - Model Visualization
    - `plot_model`

---

- **Advanced Topics**
  - Custom Losses and Metrics
    - Subclassing `tf.keras.losses.Loss`, `tf.keras.metrics.Metric`
  - Graph and Eager Execution
    - Performance tuning
  - Mixed Precision Training
    - `tf.keras.mixed_precision`
  - AutoML Integration
    - Keras Tuner
