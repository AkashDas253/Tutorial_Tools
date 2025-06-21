## **Activation Functions in TensorFlow**  

### **Overview**  
Activation functions introduce **non-linearity** in neural networks, enabling them to learn **complex patterns**. They determine the **output** of each neuron and affect training stability, speed, and accuracy.  

---

### **Types of Activation Functions**  

| **Activation Function** | **Formula** | **Range** | **Key Characteristics** | **Example Usage** |
|------------------|----------------------|----------|------------------|------------------|
| **ReLU (Rectified Linear Unit)** |$f(x) = \max(0, x)$|$[0, \infty)$| Prevents vanishing gradients; fast computation. | `tf.keras.layers.ReLU()` |
| **Leaky ReLU** |$f(x) = x \text{ if } x > 0, \text{ else } 0.01x$|$(-\infty, \infty)$| Avoids dead neurons issue in ReLU. | `tf.keras.layers.LeakyReLU(alpha=0.01)` |
| **PReLU (Parametric ReLU)** |$f(x) = x \text{ if } x > 0, \text{ else } \alpha x$|$(-\infty, \infty)$| Learns the slope$\alpha$dynamically. | `tf.keras.layers.PReLU()` |
| **ELU (Exponential Linear Unit)** |$f(x) = x \text{ if } x > 0, \text{ else } \alpha (e^x - 1)$|$(-\infty, \infty)$| Avoids vanishing gradient; smooth gradient. | `tf.keras.layers.ELU(alpha=1.0)` |
| **Sigmoid** |$f(x) = \frac{1}{1+e^{-x}}$|$(0,1)$| Used in binary classification; prone to vanishing gradient. | `tf.keras.activations.sigmoid(x)` |
| **Tanh (Hyperbolic Tangent)** |$f(x) = \frac{e^x - e^{-x}}{e^x + e^{-x}}$|$(-1,1)$| Centered around zero; used in RNNs. | `tf.keras.activations.tanh(x)` |
| **Softmax** |$f(x_i) = \frac{e^{x_i}}{\sum e^{x_j}}$|$(0,1)$| Used for multi-class classification. | `tf.keras.activations.softmax(x)` |
| **Swish** |$f(x) = x \cdot \sigma(x)$|$(-\infty, \infty)$| Smooth and non-monotonic; improves deep models. | `tf.keras.activations.swish(x)` |

---

### **1. ReLU (Rectified Linear Unit)**  
- Most commonly used activation for **deep networks**.  
- Eliminates **negative values**, speeding up convergence.  

#### **Syntax**  
```python
tf.keras.layers.ReLU()
```

#### **Example**  
```python
relu_layer = tf.keras.layers.ReLU()
output = relu_layer(input_data)
```

#### **Limitation**  
- **Dying neurons problem**: If neurons output **0** for all inputs, they **stop learning**.

---

### **2. Leaky ReLU**  
- Solves the **dying ReLU problem** by allowing **small negative values**.  

#### **Syntax**  
```python
tf.keras.layers.LeakyReLU(alpha=0.01)
```

#### **Example**  
```python
leaky_relu = tf.keras.layers.LeakyReLU(alpha=0.01)
output = leaky_relu(input_data)
```

---

### **3. PReLU (Parametric ReLU)**  
- Instead of a fixed slope for negative values, \(\alpha\) is learned during training.  

#### **Syntax**  
```python
tf.keras.layers.PReLU()
```

#### **Example**  
```python
prelu = tf.keras.layers.PReLU()
output = prelu(input_data)
```

---

### **4. ELU (Exponential Linear Unit)**  
- **Smooth gradient** prevents dead neurons.  
- More computationally expensive than ReLU.  

#### **Syntax**  
```python
tf.keras.layers.ELU(alpha=1.0)
```

#### **Example**  
```python
elu = tf.keras.layers.ELU(alpha=1.0)
output = elu(input_data)
```

---

### **5. Sigmoid**  
- Used in **binary classification** problems.  
- Prone to **vanishing gradient** for large positive/negative inputs.  

#### **Syntax**  
```python
tf.keras.activations.sigmoid(x)
```

#### **Example**  
```python
sigmoid_output = tf.keras.activations.sigmoid(input_data)
```

---

### **6. Tanh (Hyperbolic Tangent)**  
- Used in **RNNs** as it is **zero-centered**.  

#### **Syntax**  
```python
tf.keras.activations.tanh(x)
```

#### **Example**  
```python
tanh_output = tf.keras.activations.tanh(input_data)
```

---

### **7. Softmax**  
- Converts logits into **probability distribution** for multi-class classification.  

#### **Syntax**  
```python
tf.keras.activations.softmax(x)
```

#### **Example**  
```python
softmax_output = tf.keras.activations.softmax(input_data)
```

---

### **8. Swish**  
- **Non-monotonic** function developed by Google.  
- Outperforms ReLU in **deep networks**.  

#### **Syntax**  
```python
tf.keras.activations.swish(x)
```

#### **Example**  
```python
swish_output = tf.keras.activations.swish(input_data)
```

---

### **Comparison of Activation Functions**  

| **Function** | **Range** | **Zero-Centered?** | **Computational Cost** | **Gradient Issues?** | **Common Usage** |
|------------|----------|----------------|----------------|----------------|--------------|
| **ReLU** | \( [0, \infty) \) | ❌ No | Low | Dying neurons | CNNs, deep networks |
| **Leaky ReLU** | \( (-\infty, \infty) \) | ✅ Yes | Low | None | CNNs, RNNs |
| **PReLU** | \( (-\infty, \infty) \) | ✅ Yes | Medium | None | CNNs, RNNs |
| **ELU** | \( (-\infty, \infty) \) | ✅ Yes | Medium | None | CNNs, deep networks |
| **Sigmoid** | \( (0,1) \) | ❌ No | High | Vanishing gradient | Binary classification |
| **Tanh** | \( (-1,1) \) | ✅ Yes | High | Vanishing gradient | RNNs, NLP |
| **Softmax** | \( (0,1) \) | ❌ No | High | None | Multi-class classification |
| **Swish** | \( (-\infty, \infty) \) | ✅ Yes | High | None | Deep learning |

---

### **Conclusion**  
- **ReLU** is the default for **CNNs and deep networks**, but **Leaky ReLU** and **PReLU** solve its dying neuron issue.  
- **Sigmoid and Tanh** are used in **binary classification and RNNs**, but suffer from **vanishing gradient**.  
- **Softmax** is best for **multi-class classification**.  
- **Swish** and **ELU** improve learning for deep models but are more computationally expensive.