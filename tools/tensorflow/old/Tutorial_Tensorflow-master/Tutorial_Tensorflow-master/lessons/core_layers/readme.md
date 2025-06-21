## **Core Layers in TensorFlow**  

### **Overview**  
Core layers in TensorFlow are the fundamental building blocks used to create neural networks. These layers handle **data transformations, weight initialization, and activations**. They are part of the `tf.keras.layers` module.  

---

### **Types of Core Layers**  

| **Layer Type** | **Description** | **Example Usage** |
|--------------|-----------------|------------------|
| **Dense** | Fully connected (FC) layer with learned weights. | `tf.keras.layers.Dense(64, activation='relu')` |
| **Activation** | Applies an activation function to inputs. | `tf.keras.layers.Activation('relu')` |
| **Embedding** | Converts integer indices into dense vectors (used for NLP). | `tf.keras.layers.Embedding(input_dim=1000, output_dim=64)` |
| **Lambda** | Wraps a custom function inside a layer. | `tf.keras.layers.Lambda(lambda x: x * 2)` |

---

### **1. Dense Layer**  
- **Fully connected (FC) layer** that applies a weight matrix and bias.  
- Used in most feedforward networks.  
- Supports activation functions.  

#### **Syntax**  
```python
tf.keras.layers.Dense(units, activation=None, use_bias=True, kernel_initializer='glorot_uniform')
```

#### **Example**  
```python
dense_layer = tf.keras.layers.Dense(64, activation='relu')
output = dense_layer(input_data)
```

---

### **2. Activation Layer**  
- Applies an activation function to its input.  
- Can be used separately or inside a Dense layer.  

#### **Syntax**  
```python
tf.keras.layers.Activation(activation)
```

#### **Example**  
```python
act_layer = tf.keras.layers.Activation('relu')
output = act_layer(input_data)
```
OR  
```python
tf.keras.layers.Dense(64, activation='relu')
```

---

### **3. Embedding Layer**  
- Maps categorical data (word indices) to dense vector representations.  
- Commonly used in **NLP tasks**.  

#### **Syntax**  
```python
tf.keras.layers.Embedding(input_dim, output_dim, input_length=None)
```

#### **Example**  
```python
embedding_layer = tf.keras.layers.Embedding(input_dim=1000, output_dim=64)
output = embedding_layer(input_data)
```

---

### **4. Lambda Layer**  
- Wraps any function inside a layer.  
- Used for applying **custom transformations**.  

#### **Syntax**  
```python
tf.keras.layers.Lambda(function)
```

#### **Example**  
```python
lambda_layer = tf.keras.layers.Lambda(lambda x: x * 2)
output = lambda_layer(input_data)
```

---

### **Comparison of Core Layers**  

| **Feature** | **Dense** | **Activation** | **Embedding** | **Lambda** |
|------------|---------|-------------|-----------|---------|
| **Trainable Parameters** | ✅ Yes | ❌ No | ✅ Yes | ❌ No |
| **Supports Activation** | ✅ Yes | ✅ Yes | ❌ No | ❌ No |
| **Use Case** | FC layers | Activation functions | NLP (word embeddings) | Custom functions |
| **Input Type** | Any Tensor | Any Tensor | Integer Indices | Any Tensor |

---

### **Conclusion**  
- **Dense layers** are used in fully connected networks.  
- **Activation layers** apply non-linearity.  
- **Embedding layers** map categorical data to dense vectors.  
- **Lambda layers** allow for custom functions.