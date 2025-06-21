## Building Models in TensorFlow

TensorFlow provides flexible APIs for creating machine learning models. The primary approaches include **Sequential API**, **Functional API**, and **Subclassing API**.

---

#### **1. Sequential API**

The `tf.keras.Sequential` API is ideal for building models layer-by-layer, where each layer has exactly one input and one output.

| **Feature**      | **Description**                                             | **Example Code**                                                                                     |
|------------------|-------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| **Linear Stack** | Layers are added sequentially.                              | ```python<br>model = tf.keras.Sequential([tf.keras.layers.Dense(64, activation='relu'), tf.keras.layers.Dense(1)])``` |
| **Simplified Syntax** | Layers can also be added using `.add()`.                  | ```python<br>model = tf.keras.Sequential()<br>model.add(tf.keras.layers.Dense(64, activation='relu'))``` |

**Usage Example:**

```python
from tensorflow.keras import Sequential
from tensorflow.keras.layers import Dense

# Build a simple model
model = Sequential([
    Dense(128, activation='relu', input_shape=(10,)),
    Dense(64, activation='relu'),
    Dense(1, activation='sigmoid')
])

model.summary()
```

---

#### **2. Functional API**

The `tf.keras.Model` Functional API enables the creation of complex models, such as multi-input or multi-output architectures.

| **Feature**              | **Description**                                         | **Example Code**                                                                                     |
|--------------------------|---------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| **Layer Connections**    | Define flexible connections between layers.             | ```python<br>inputs = tf.keras.Input(shape=(10,))<br>x = tf.keras.layers.Dense(64)(inputs)<br>outputs = tf.keras.layers.Dense(1)(x)<br>model = tf.keras.Model(inputs, outputs)``` |
| **Custom Architectures** | Build architectures like residual networks or shared layers.| Reuse layers or define non-linear graphs. |

**Usage Example:**

```python
from tensorflow.keras import Input, Model
from tensorflow.keras.layers import Dense, Dropout

# Define inputs and layers
inputs = Input(shape=(10,))
x = Dense(64, activation='relu')(inputs)
x = Dropout(0.5)(x)
outputs = Dense(1, activation='sigmoid')(x)

# Build the model
model = Model(inputs, outputs)

model.summary()
```

---

#### **3. Subclassing API**

For maximum flexibility, subclass `tf.keras.Model` to define custom forward passes and architectures.

| **Feature**              | **Description**                                            | **Example Code**                                                                                      |
|--------------------------|------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| **Custom Forward Pass**  | Define custom computation in the `call()` method.           | ```python<br>class MyModel(tf.keras.Model):<br>    def __init__(self):<br>        super().__init__()<br>        self.dense = tf.keras.layers.Dense(64)<br>    def call(self, inputs):<br>        return self.dense(inputs)<br>model = MyModel()``` |
| **Advanced Flexibility** | Ideal for non-standard models and research experimentation. | Use loops or conditionals in `call()`.                                                               |

**Usage Example:**

```python
from tensorflow.keras import Model
from tensorflow.keras.layers import Dense

class CustomModel(Model):
    def __init__(self):
        super(CustomModel, self).__init__()
        self.dense1 = Dense(64, activation='relu')
        self.dense2 = Dense(1, activation='sigmoid')

    def call(self, inputs):
        x = self.dense1(inputs)
        return self.dense2(x)

# Instantiate and build model
model = CustomModel()

# Forward pass example
import numpy as np
data = np.random.rand(5, 10)  # 5 samples, 10 features
print(model(data))
```

---

#### **4. Model Compilation**

All models, regardless of how they are built, must be compiled before training.

| **Step**        | **Description**                                        | **Example Code**                                                                                     |
|------------------|-------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| **Optimizer**    | Optimization algorithm (e.g., `adam`, `sgd`).         | `optimizer='adam'`                                                                                  |
| **Loss Function**| Function to minimize (e.g., `mse`, `binary_crossentropy`). | `loss='binary_crossentropy'`                                                                        |
| **Metrics**      | Metrics to monitor (e.g., `accuracy`).                | `metrics=['accuracy']`                                                                              |

```python
model.compile(optimizer='adam', loss='binary_crossentropy', metrics=['accuracy'])
```

---

#### **5. Training the Model**

| **Method**         | **Description**                                             | **Example Code**                                                                                      |
|---------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| **`fit`**          | Train the model on a dataset.                               | `model.fit(x_train, y_train, epochs=10, batch_size=32)`                                              |
| **`evaluate`**      | Evaluate the model performance on test data.               | `model.evaluate(x_test, y_test)`                                                                     |
| **`predict`**       | Generate predictions from the model.                       | `predictions = model.predict(new_data)`                                                              |

---

#### **6. Advanced Features**

| **Feature**              | **Description**                                                              | **Example Code**                                                                                      |
|--------------------------|------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| **Callbacks**            | Stop training early, save checkpoints, or adjust learning rates.            | `tf.keras.callbacks.EarlyStopping(monitor='val_loss')`                                               |
| **Custom Loss/Metric**   | Define custom logic for losses or metrics.                                  | ```python<br>def custom_loss(y_true, y_pred):<br>    return tf.reduce_mean(tf.square(y_true - y_pred))``` |
| **Save/Load Models**     | Save models for deployment or further training.                             | `model.save('model.h5')` / `model = tf.keras.models.load_model('model.h5')`                          |
