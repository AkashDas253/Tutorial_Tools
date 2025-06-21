## **Functional API in TensorFlow/Keras**

The **Functional API** in TensorFlow/Keras is a more flexible way to define complex models compared to the **Sequential API**. It allows you to define models that have multiple inputs, multiple outputs, shared layers, non-linear connections, and more. The Functional API provides more control over the architecture of the model and is suitable for complex neural networks.

---

### **Basic Structure and Overview**

In the Functional API, you define the input and output layers explicitly and then connect them through a directed acyclic graph (DAG) of layers. This is particularly useful for models with multiple branches, skip connections, and more intricate architectures.

#### **Syntax:**
```python
from tensorflow.keras import layers, models

# Define the Input layer
input_tensor = layers.Input(shape=(64,))  # Example input with 64 features

# Define a hidden layer
x = layers.Dense(64, activation='relu')(input_tensor)

# Define an output layer
output_tensor = layers.Dense(10, activation='softmax')(x)

# Create a model using the input and output tensors
model = models.Model(inputs=input_tensor, outputs=output_tensor)

# Compile the model
model.compile(optimizer='adam', loss='categorical_crossentropy', metrics=['accuracy'])
```

---

### **Key Concepts and Parameters**

| **Parameter**           | **Description**                                                                                       | **Syntax Example**                   |
|-------------------------|-------------------------------------------------------------------------------------------------------|--------------------------------------|
| **Input Layer**          | Defined explicitly using `Input()`, this serves as the entry point for the model. It requires the input shape. | `input_tensor = layers.Input(shape=(64,))` |
| **Layer Definitions**    | Layers are defined as function calls and connected via parentheses. The output of one layer becomes the input to the next. | `x = layers.Dense(64, activation='relu')(input_tensor)` |
| **Model Creation**       | A model is created by passing the input and output tensors to the `Model()` function.                 | `model = models.Model(inputs=input_tensor, outputs=output_tensor)` |
| **Output Layer**         | The final layer(s) in the model, defining the number of classes or units in the output layer.          | `output_tensor = layers.Dense(10, activation='softmax')(x)` |
| **Model Compilation**    | The `compile()` method is used to configure the model for training.                                   | `model.compile(optimizer='adam', loss='categorical_crossentropy')` |

---

### **Example 1: Simple Feedforward Neural Network (FNN)**

This example demonstrates how to build a simple neural network using the Functional API.

```python
from tensorflow.keras import layers, models

# Define the input
input_tensor = layers.Input(shape=(64,))  # 64 features

# Define the hidden layer
x = layers.Dense(64, activation='relu')(input_tensor)

# Define the output layer (classification)
output_tensor = layers.Dense(10, activation='softmax')(x)  # 10 classes for classification

# Create the model
model = models.Model(inputs=input_tensor, outputs=output_tensor)

# Compile the model
model.compile(optimizer='adam', loss='categorical_crossentropy', metrics=['accuracy'])
```

---

### **Example 2: Multi-Input Model**

In this example, we have two different inputs to the model. The Functional API allows us to create models that can take multiple inputs.

```python
from tensorflow.keras import layers, models

# Define two input layers
input1 = layers.Input(shape=(64,))
input2 = layers.Input(shape=(32,))

# Define a shared hidden layer
x1 = layers.Dense(64, activation='relu')(input1)
x2 = layers.Dense(64, activation='relu')(input2)

# Combine the two branches
combined = layers.concatenate([x1, x2])

# Add a final output layer
output = layers.Dense(10, activation='softmax')(combined)

# Create the model
model = models.Model(inputs=[input1, input2], outputs=output)

# Compile the model
model.compile(optimizer='adam', loss='categorical_crossentropy', metrics=['accuracy'])
```

---

### **Example 3: Model with Shared Layers**

The Functional API supports shared layers, where the same layer is applied to different inputs or parts of the model. This is useful in situations like Siamese Networks or multi-task learning.

```python
from tensorflow.keras import layers, models

# Define the input layers
input1 = layers.Input(shape=(64,))
input2 = layers.Input(shape=(64,))

# Define a shared Dense layer
shared_dense = layers.Dense(64, activation='relu')

# Apply the shared layer to both inputs
output1 = shared_dense(input1)
output2 = shared_dense(input2)

# Combine the outputs
merged = layers.concatenate([output1, output2])

# Define the final output layer
final_output = layers.Dense(1, activation='sigmoid')(merged)

# Create the model
model = models.Model(inputs=[input1, input2], outputs=final_output)

# Compile the model
model.compile(optimizer='adam', loss='binary_crossentropy', metrics=['accuracy'])
```

---

### **Example 4: Skip Connections (Residual Network)**

The Functional API also allows you to create skip connections, which are essential in residual networks (ResNets).

```python
from tensorflow.keras import layers, models

# Define the input layer
input_tensor = layers.Input(shape=(64,))

# First hidden layer
x = layers.Dense(64, activation='relu')(input_tensor)

# Add a skip connection
skip = layers.Dense(64, activation='relu')(x)

# Add another layer and connect the skip connection
x = layers.add([x, skip])

# Output layer
output_tensor = layers.Dense(10, activation='softmax')(x)

# Create the model
model = models.Model(inputs=input_tensor, outputs=output_tensor)

# Compile the model
model.compile(optimizer='adam', loss='categorical_crossentropy', metrics=['accuracy'])
```

---

### **Key Parameters and Methods**

#### **Layer Parameters**
Each layer in the Functional API can accept various parameters depending on the layer type (e.g., `Dense`, `Conv2D`, `LSTM`), such as:
- **units**: Number of neurons in the layer.
- **activation**: Activation function applied after the layer’s transformation.
- **input_shape**: Shape of the input data (required only for the first layer).
- **kernel_initializer**: Initializer for the layer's weights.
- **bias_initializer**: Initializer for the bias.

#### **Common Methods**
- **Input()**: Used to define an input tensor to the model.
  ```python
  input_tensor = layers.Input(shape=(64,))
  ```

- **Model()**: Defines the model by passing the input and output tensors.
  ```python
  model = models.Model(inputs=input_tensor, outputs=output_tensor)
  ```

- **compile()**: Configures the model for training.
  ```python
  model.compile(optimizer='adam', loss='categorical_crossentropy', metrics=['accuracy'])
  ```

- **fit()**: Trains the model on the given data.
  ```python
  model.fit(x_train, y_train, epochs=10, batch_size=32)
  ```

---

### **Advantages of the Functional API**
- **Flexibility**: Allows more complex architectures (e.g., models with multiple inputs and outputs, shared layers).
- **Non-linear Connections**: Easily create models with non-linear connections such as skip connections and residual blocks.
- **Shared Layers**: Enables the reuse of layers for different parts of the network, useful for multi-task learning or Siamese networks.

### **Limitations**
- **Complexity**: May feel more complex compared to the Sequential API, especially for simple models.
- **Requires more code**: More lines of code are needed to build models compared to the Sequential API.

---

### **Conclusion**
The **Functional API** in TensorFlow/Keras provides flexibility and control for creating complex neural networks. It is suitable for models with multiple inputs, multiple outputs, shared layers, and non-linear architectures. If you need to create more sophisticated models than the Sequential API allows, the Functional API is the right choice.