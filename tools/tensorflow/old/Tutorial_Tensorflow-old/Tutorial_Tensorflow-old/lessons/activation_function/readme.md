## **Activation Functions in Keras**  
Activation functions are mathematical functions applied to neurons in neural networks to introduce non-linearity. Here's a detailed list of commonly used activation functions in Keras, their syntax, parameters, and descriptions:

---

### **Activation Functions**

| **Function**       | **Description**                                                                                                  | **Parameters**                                   | **Syntax**                         | **Example**                       |
|---------------------|------------------------------------------------------------------------------------------------------------------|------------------------------------------------|------------------------------------|------------------------------------|
| **ReLU**            | Rectified Linear Unit: Outputs input directly if positive; otherwise, outputs 0.                               | - None                                         | `'relu'`                           | `Dense(64, activation='relu')`    |
| **Sigmoid**         | Maps input to a range between 0 and 1.                                                                          | - None                                         | `'sigmoid'`                        | `Dense(1, activation='sigmoid')`  |
| **Tanh**            | Maps input to a range between -1 and 1.                                                                         | - None                                         | `'tanh'`                           | `Dense(64, activation='tanh')`    |
| **Softmax**         | Converts a vector of numbers into probabilities summing to 1.                                                  | - None                                         | `'softmax'`                        | `Dense(10, activation='softmax')` |
| **Softplus**        | Smooth approximation of ReLU, outputs `log(1 + exp(x))`.                                                       | - None                                         | `'softplus'`                       | `Dense(64, activation='softplus')`|
| **Softsign**        | Maps input to a range between -1 and 1, like `tanh`, but with slower gradient saturation.                       | - None                                         | `'softsign'`                       | `Dense(64, activation='softsign')`|
| **Exponential**     | Exponentiates the input, i.e., `exp(x)`.                                                                       | - None                                         | `'exponential'`                    | `Dense(64, activation='exponential')` |
| **ELU**             | Exponential Linear Unit: Outputs input if positive; outputs exponential decay for negative input.              | - `alpha (float)`: Scaling factor (`1.0`)      | `'elu'`                            | `Dense(64, activation='elu')`     |
| **SELU**            | Scaled Exponential Linear Unit: Scales ELU to maintain self-normalizing properties.                            | - None                                         | `'selu'`                           | `Dense(64, activation='selu')`    |
| **Leaky ReLU**      | Allows a small, non-zero gradient for negative inputs to prevent dead neurons.                                 | - `alpha (float)`: Slope for negative inputs (`0.3`) | `LeakyReLU(alpha=0.3)`             | `LeakyReLU(alpha=0.3)`            |
| **Thresholded ReLU**| Thresholded Linear Unit: Outputs input if greater than a threshold; otherwise, outputs 0.                      | - `theta (float)`: Threshold value (`1.0`)     | `ThresholdedReLU(theta=1.0)`       | `ThresholdedReLU(theta=1.0)`      |
| **Hard Sigmoid**    | Approximation of sigmoid function for computational efficiency.                                                | - None                                         | `'hard_sigmoid'`                   | `Dense(64, activation='hard_sigmoid')` |
| **Swish**           | Self-gated activation function, `x * sigmoid(x)`.                                                              | - None                                         | `'swish'`                          | `Dense(64, activation='swish')`   |
| **GELU**            | Gaussian Error Linear Unit: Smooth approximation of ReLU with probabilistic behavior.                          | - None                                         | `'gelu'`                           | `Dense(64, activation='gelu')`    |

---

### **Custom Activation Functions**
Keras also allows defining custom activation functions using Python functions.

#### Example:
```python
from tensorflow.keras.layers import Dense
import tensorflow as tf

# Custom activation function: x^2
def custom_activation(x):
    return tf.square(x)

# Applying custom activation
Dense(64, activation=custom_activation)
```

---

### **Comparison of Activation Functions**

| **Function**      | **Range**      | **Use Case**                                                                                           |
|--------------------|----------------|-------------------------------------------------------------------------------------------------------|
| **ReLU**          | `[0, ∞)`       | Default for most hidden layers; avoids vanishing gradients.                                           |
| **Sigmoid**       | `(0, 1)`       | For binary classification outputs.                                                                   |
| **Tanh**          | `(-1, 1)`      | For symmetric outputs; generally used in RNNs.                                                       |
| **Softmax**       | `[0, 1]`       | For multi-class classification.                                                                      |
| **Leaky ReLU**    | `(-∞, ∞)`      | Mitigates "dead neurons" issue in ReLU.                                                              |
| **SELU**          | `(-∞, ∞)`      | For self-normalizing neural networks.                                                               |
| **Swish**         | `(-∞, ∞)`      | Improves deep network training performance.                                                          |

---


### **Custom Activation Functions in TensorFlow/Keras**  

In addition to the built-in activation functions, TensorFlow/Keras allows defining **custom activation functions** to meet specific requirements. Below is a comprehensive guide to creating and using custom activation functions.

---

### **Creating Custom Activation Functions**

#### 1. **Using Python Functions**
A simple Python function can be used as an activation function.  

| **Syntax**                  | **Parameters**                     | **Description**                            |
|-----------------------------|-------------------------------------|--------------------------------------------|
| `def custom_activation(x):` | `x` (Tensor): Input tensor.         | Defines the transformation on input tensor. |

##### Example:
```python
from tensorflow.keras.layers import Dense
import tensorflow as tf

# Define custom activation
def custom_activation(x):
    return tf.square(x)  # Output: x^2

# Use in Dense layer
Dense(64, activation=custom_activation)
```

---

#### 2. **Using Lambda Layers**
If the custom activation is simple, it can be implemented using a **Lambda layer**.

| **Syntax**             | **Parameters**                     | **Description**                            |
|------------------------|-------------------------------------|--------------------------------------------|
| `Lambda(function)`     | `function`: Transformation function | Creates a layer for custom transformations. |

##### Example:
```python
from tensorflow.keras.layers import Lambda

# Define activation in Lambda
custom_layer = Lambda(lambda x: tf.maximum(x, 0.1 * x))  # Leaky ReLU example
```

---

#### 3. **Using `tf.keras.layers.Layer` for Complex Activation**
For more complex operations requiring additional parameters, you can create a custom layer by subclassing `tf.keras.layers.Layer`.

| **Syntax**              | **Parameters**                                    | **Description**                            |
|-------------------------|--------------------------------------------------|--------------------------------------------|
| `class CustomLayer(Layer):` | `call(inputs)`: Define forward pass logic.      | Implements custom activations as layers.   |

##### Example:
```python
from tensorflow.keras.layers import Layer

# Custom activation as a layer
class CustomActivation(Layer):
    def call(self, inputs):
        return tf.nn.relu(inputs) - tf.nn.relu(inputs - 6)  # Example: Clipped ReLU

# Use in model
custom_activation_layer = CustomActivation()
```

---

### **Using Custom Activation Functions**

| **Method**                   | **How to Use**                                                                 |
|------------------------------|-------------------------------------------------------------------------------|
| **In Dense Layer**           | Pass the custom function to the `activation` parameter of the layer.          |
| **As a Separate Layer**      | Use `Lambda` or a subclassed `Layer` to define a layer performing activation. |

---

### **Examples of Custom Activations**

| **Custom Activation**  | **Code**                                                                                   | **Description**                     |
|-------------------------|-------------------------------------------------------------------------------------------|-------------------------------------|
| Square Function         | `return tf.square(x)`                                                                     | Squares the input (`x^2`).         |
| Leaky ReLU              | `return tf.maximum(x, alpha * x)`                                                         | Allows a small gradient for `x < 0`. |
| Exponential Decay       | `return tf.exp(-x)`                                                                       | Exponential decay on input values. |
| Parametric ReLU (PReLU) | `return tf.where(x > 0, x, alpha * x)`                                                    | Adds trainable slope for negatives. |
| Custom Clipping         | `return tf.clip_by_value(x, clip_value_min=0, clip_value_max=1)`                          | Clips values between 0 and 1.      |

---

### **Advanced Example: Parametric ReLU (PReLU)**  
A learnable activation function with parameters for negative slope.

```python
from tensorflow.keras.layers import Layer
import tensorflow as tf

class ParametricReLU(Layer):
    def __init__(self, **kwargs):
        super(ParametricReLU, self).__init__(**kwargs)
        self.alpha = None  # Trainable parameter

    def build(self, input_shape):
        # Initialize alpha
        self.alpha = self.add_weight(
            shape=(input_shape[-1],),
            initializer="zeros",
            trainable=True,
            name="alpha"
        )
    
    def call(self, inputs):
        return tf.where(inputs > 0, inputs, self.alpha * inputs)

# Example usage
layer = ParametricReLU()
```

---
