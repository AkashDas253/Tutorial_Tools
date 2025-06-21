# Keras

---

## What is Keras?

Keras is a **high-level deep learning API** integrated into TensorFlow (`tf.keras`) that simplifies the process of building, training, evaluating, and deploying neural networks.

* Originally a separate library, now **part of TensorFlow core** since TF 2.x
* Abstracts low-level details while providing flexibility and modularity

---

## Core Features

| Feature       | Description                                                 |
| ------------- | ----------------------------------------------------------- |
| User-friendly | Simple, consistent APIs for common use cases                |
| Modular       | Composable architecture: layers, models, optimizers, etc.   |
| Pythonic      | Intuitive and easy-to-read syntax                           |
| Scalable      | Works with TPUs, GPUs, and across multiple devices          |
| Integrated    | Comes with `tf.keras`, TensorFlow's official high-level API |

---

## Major Components of Keras

### 1. Models (`tf.keras.Model`)

* Represents a complete model
* Two primary ways to define models:

  * **Sequential API**
  * **Functional API**
  * **Model Subclassing**

### 2. Layers (`tf.keras.layers`)

* Fundamental building blocks of models
* Examples:

  * Core: `Dense`, `Dropout`, `Flatten`
  * Convolutional: `Conv2D`, `Conv1D`
  * Recurrent: `LSTM`, `GRU`
  * Normalization: `BatchNormalization`
  * Attention: `MultiHeadAttention`

### 3. Optimizers (`tf.keras.optimizers`)

* Algorithms for updating model weights during training
* Common options: `SGD`, `Adam`, `RMSprop`, `Adagrad`

### 4. Losses (`tf.keras.losses`)

* Functions that measure prediction error
* Examples:

  * Classification: `BinaryCrossentropy`, `CategoricalCrossentropy`
  * Regression: `MeanSquaredError`, `Huber`

### 5. Metrics (`tf.keras.metrics`)

* Monitor model performance
* Built-in: `Accuracy`, `Precision`, `Recall`, `AUC`

### 6. Callbacks (`tf.keras.callbacks`)

* Used to monitor and control training process
* Common callbacks:

  * `EarlyStopping`
  * `ModelCheckpoint`
  * `ReduceLROnPlateau`
  * `TensorBoard`

---

## Model Building Approaches

### Sequential API

```python
model = tf.keras.Sequential([
    tf.keras.layers.Dense(64, activation='relu'),
    tf.keras.layers.Dense(10)
])
```

### Functional API

```python
inputs = tf.keras.Input(shape=(784,))
x = tf.keras.layers.Dense(64, activation='relu')(inputs)
outputs = tf.keras.layers.Dense(10)(x)
model = tf.keras.Model(inputs, outputs)
```

### Subclassing API

```python
class MyModel(tf.keras.Model):
    def __init__(self):
        super().__init__()
        self.dense1 = tf.keras.layers.Dense(64, activation='relu')
        self.dense2 = tf.keras.layers.Dense(10)
    def call(self, inputs):
        x = self.dense1(inputs)
        return self.dense2(x)
model = MyModel()
```

---

## Training Workflow

```python
model.compile(
    optimizer='adam',
    loss='sparse_categorical_crossentropy',
    metrics=['accuracy']
)

model.fit(x_train, y_train, epochs=5, batch_size=32)
model.evaluate(x_test, y_test)
model.predict(new_data)
```

---

## Model Saving and Loading

### Save

* Entire model:

  ```python
  model.save('model_path')
  ```
* Only weights:

  ```python
  model.save_weights('weights.h5')
  ```

### Load

* Entire model:

  ```python
  tf.keras.models.load_model('model_path')
  ```
* Only weights:

  ```python
  model.load_weights('weights.h5')
  ```

---

## Keras Tuner

* Hyperparameter tuning library for Keras models
* Automatically searches optimal layer sizes, learning rates, etc.

---

## Integration with TensorFlow Ecosystem

| Component         | Integration in Keras                          |
| ----------------- | --------------------------------------------- |
| `tf.data`         | Custom input pipelines                        |
| `tf.function`     | Performance optimization with graph execution |
| `tf.distribute`   | Distributed training support                  |
| TensorBoard       | Logging via `TensorBoard` callback            |
| SavedModel format | Export and deploy models                      |
| TensorFlow Lite   | Convert Keras models to run on edge devices   |

---

## Use Cases

* Image classification (e.g., CNNs)
* Text classification and generation (e.g., RNNs, Transformers)
* Time series forecasting
* GANs and autoencoders
* Multi-modal networks
* Transfer learning and fine-tuning

---

## Summary

| Aspect           | Benefit                                     |
| ---------------- | ------------------------------------------- |
| Ease of use      | Simplified API for rapid prototyping        |
| Flexibility      | Functional and subclassing APIs available   |
| Scalability      | Run on CPUs, GPUs, TPUs                     |
| Extensibility    | Custom layers, losses, and metrics possible |
| Production-ready | Integrates with full TensorFlow stack       |

---
