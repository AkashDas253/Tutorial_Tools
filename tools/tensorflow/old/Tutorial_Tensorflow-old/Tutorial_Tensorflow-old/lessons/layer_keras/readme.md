## **Keras Layers in TensorFlow**  
Below is a comprehensive list of major Keras layers in TensorFlow, their parameters, descriptions, and syntax. This serves as a quick reference for understanding layer types, parameters, and usage.  

---

### **Core Layers**

| **Layer**   | **Description**                                                                 | **Key Parameters**                                                                                                                                          | **Syntax**                              |
|-------------|---------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------|
| **Dense**   | Fully connected layer, commonly used in feedforward neural networks.            | - `units (int)`: Number of neurons in the layer<br>- `activation (str)`: Activation function (`None`)<br>- `use_bias (bool)`: Include bias (`True`)          | `Dense(units=64, activation='relu')`    |
| **Dropout** | Randomly sets input units to 0 during training to prevent overfitting.          | - `rate (float)`: Fraction of inputs to drop (`0.5`)                                                                                                       | `Dropout(rate=0.5)`                     |
| **Flatten** | Flattens the input without affecting the batch size.                            | None                                                                                                                                                        | `Flatten()`                             |
| **Activation** | Applies an activation function to the input.                                | - `activation (str)`: Name of activation function                                                                                                          | `Activation('relu')`                    |
| **Reshape** | Reshapes the input to a specified shape.                                        | - `target_shape (tuple)`: Target shape                                                                                                                     | `Reshape(target_shape=(2, 3))`          |

---

### **Convolutional Layers**

| **Layer**       | **Description**                                                                | **Key Parameters**                                                                                                                                                                                                                                              | **Syntax**                                        |
|------------------|--------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------|
| **Conv1D**       | 1D convolution layer for sequence data.                                        | - `filters (int)`: Number of output filters<br>- `kernel_size (int or tuple)`: Convolution window size<br>- `strides (int)`: Step size (`1`)<br>- `padding (str)`: Padding type (`'valid'`)<br>- `activation (str)`: Activation function (`None`)             | `Conv1D(filters=32, kernel_size=3, activation='relu')` |
| **Conv2D**       | 2D convolution layer for image data.                                           | - `filters (int)`: Number of output filters<br>- `kernel_size (int or tuple)`: Convolution window size<br>- `strides (tuple)`: Step size (`(1, 1)`)<br>- `padding (str)`: Padding type (`'valid'`)<br>- `activation (str)`: Activation function (`None`)    | `Conv2D(filters=32, kernel_size=(3, 3), activation='relu')` |
| **Conv3D**       | 3D convolution layer for volumetric data.                                      | - Similar to `Conv2D` but applies to 3D inputs                                                                                                                                                                           | `Conv3D(filters=32, kernel_size=(3, 3, 3))`       |
| **SeparableConv2D** | Depthwise separable 2D convolution layer.                                  | - Similar to `Conv2D` but separates spatial and depth operations.                                                                                                                                                       | `SeparableConv2D(filters=32, kernel_size=3)`      |
| **Conv2DTranspose** | Transposed 2D convolution for upsampling (deconvolution).                  | - Similar to `Conv2D`                                                                                                                                                                                                   | `Conv2DTranspose(filters=32, kernel_size=(3, 3))`|

---

### **Pooling Layers**

| **Layer**         | **Description**                                                                | **Key Parameters**                                                                                                                                   | **Syntax**                                      |
|--------------------|--------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------|
| **MaxPooling1D**   | 1D max pooling for sequence data.                                              | - `pool_size (int)`: Downscale factor<br>- `strides (int)`: Step size<br>- `padding (str)`: Padding type (`'valid'`)                                  | `MaxPooling1D(pool_size=2)`                   |
| **MaxPooling2D**   | 2D max pooling for image data.                                                 | - `pool_size (tuple)`: Downscale factor<br>- Similar to `MaxPooling1D`                                                                               | `MaxPooling2D(pool_size=(2, 2))`              |
| **AveragePooling2D** | 2D average pooling for image data.                                          | - Similar to `MaxPooling2D`                                                                                                                          | `AveragePooling2D(pool_size=(2, 2))`          |
| **GlobalMaxPooling2D** | Reduces input along spatial dimensions to maximum values for each feature. | None                                                                                                                                                 | `GlobalMaxPooling2D()`                        |

---

### **Recurrent Layers**

| **Layer**    | **Description**                                                                                          | **Key Parameters**                                                                                                                                                         | **Syntax**                          |
|--------------|----------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
| **LSTM**     | Long Short-Term Memory layer for sequence data.                                                          | - `units (int)`: Number of LSTM units<br>- `activation (str)`: Activation function (`'tanh'`)<br>- `return_sequences (bool)`: Return full sequence (`False`)               | `LSTM(units=64, return_sequences=True)` |
| **GRU**      | Gated Recurrent Unit layer for sequence data.                                                            | - Similar to `LSTM` but simpler architecture.                                                                                                                             | `GRU(units=64)`                      |
| **SimpleRNN** | Basic fully connected RNN layer.                                                                        | - Similar to `LSTM` but without gating mechanisms.                                                                                                                        | `SimpleRNN(units=64)`                |

---

### **Normalization Layers**

| **Layer**             | **Description**                                                          | **Key Parameters**                                                                                                                                  | **Syntax**                            |
|------------------------|--------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------|
| **BatchNormalization** | Normalizes the inputs of a layer to improve stability and performance.  | - `axis (int)`: Axis to normalize (`-1`)                                                                                                            | `BatchNormalization()`                |
| **LayerNormalization** | Normalizes inputs across features for improved training.                | - Similar to `BatchNormalization`                                                                                                                  | `LayerNormalization()`                |

---

### **Advanced Layers**

| **Layer**        | **Description**                                                                                        | **Key Parameters**                                                                                                                                            | **Syntax**                                  |
|-------------------|--------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------|
| **Embedding**     | Converts categorical data into dense vectors of fixed size, useful in NLP.                            | - `input_dim (int)`: Vocabulary size<br>- `output_dim (int)`: Dimension of embedding vectors                                                                  | `Embedding(input_dim=1000, output_dim=64)`  |
| **Attention**     | Applies attention mechanisms to improve sequence modeling.                                            | - `use_scale (bool)`: Scale query mechanism                                                                                                                   | `Attention()`                               |
| **TimeDistributed** | Applies a layer to every temporal slice of an input.                                               | - Pass a layer inside                                                                                                                                        | `TimeDistributed(Dense(64))`               |
| **Add**           | Element-wise addition of inputs.                                                                      | None                                                                                                                                                          | `Add()([input1, input2])`                   |

---

### **Example Usage**

```python
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense, Dropout, Conv2D, Flatten, MaxPooling2D

# Build a simple CNN
model = Sequential([
    Conv2D(filters=32, kernel_size=(3, 3), activation='relu', input_shape=(64, 64, 3)),
    MaxPooling2D(pool_size=(2, 2)),
    Flatten(),
    Dense(units=128, activation='relu'),
    Dropout(rate=0.5),
    Dense(units=10, activation='softmax')
])

model.summary()
```  
