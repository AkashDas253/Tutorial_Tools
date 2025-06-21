## **Optimizers in TensorFlow**  

### **Overview**  
Optimizers in TensorFlow adjust the model's parameters to minimize the **loss function** during training. They use **gradients** to update weights, influencing convergence speed and accuracy.

---

### **Types of Optimizers**  

| **Optimizer** | **Formula** | **Key Features** | **Usage in TensorFlow** |
|--------------|------------|------------------|-------------------------|
| **SGD (Stochastic Gradient Descent)** | \( w = w - \eta \nabla L(w) \) | Simple, good for convex problems, slow for large datasets | `tf.keras.optimizers.SGD(learning_rate=0.01)` |
| **Momentum** | \( v_t = \gamma v_{t-1} + \eta \nabla L(w) \)  \( w = w - v_t \) | Helps escape local minima, reduces oscillations | `tf.keras.optimizers.SGD(learning_rate=0.01, momentum=0.9)` |
| **Nesterov Accelerated Gradient (NAG)** | \( v_t = \gamma v_{t-1} + \eta \nabla L(w - \gamma v_{t-1}) \) | Better convergence than Momentum | `tf.keras.optimizers.SGD(learning_rate=0.01, momentum=0.9, nesterov=True)` |
| **Adagrad** | \( G_t = G_{t-1} + \nabla L(w)^2 \) \( w = w - \frac{\eta}{\sqrt{G_t} + \epsilon} \nabla L(w) \) | Adaptive learning rate per parameter | `tf.keras.optimizers.Adagrad(learning_rate=0.01)` |
| **RMSprop** | \( G_t = \beta G_{t-1} + (1 - \beta) \nabla L(w)^2 \) \( w = w - \frac{\eta}{\sqrt{G_t} + \epsilon} \nabla L(w) \) | Prevents diminishing learning rate issues | `tf.keras.optimizers.RMSprop(learning_rate=0.001, rho=0.9)` |
| **Adam** | Combines Momentum and RMSprop | Adaptive learning rate, widely used | `tf.keras.optimizers.Adam(learning_rate=0.001, beta_1=0.9, beta_2=0.999)` |
| **AdaMax** | Variant of Adam with infinity norm | Stable updates | `tf.keras.optimizers.Adamax(learning_rate=0.002)` |
| **Nadam** | Combines Adam and Nesterov | Faster convergence | `tf.keras.optimizers.Nadam(learning_rate=0.002)` |
| **FTRL (Follow The Regularized Leader)** | L1 and L2 regularization | Used in large-scale linear models | `tf.keras.optimizers.Ftrl(learning_rate=0.01)` |

---

### **1. Stochastic Gradient Descent (SGD)**
- Updates weights using **gradient of a single batch**.  
- **Can be slow** due to oscillations.  

#### **Syntax**
```python
tf.keras.optimizers.SGD(learning_rate=0.01)
```

#### **Example**
```python
optimizer = tf.keras.optimizers.SGD(learning_rate=0.01)
```

---

### **2. Momentum**
- Adds **velocity** to weight updates to prevent oscillations.  
- Faster than standard SGD.  

#### **Syntax**
```python
tf.keras.optimizers.SGD(learning_rate=0.01, momentum=0.9)
```

#### **Example**
```python
optimizer = tf.keras.optimizers.SGD(learning_rate=0.01, momentum=0.9)
```

---

### **3. Nesterov Accelerated Gradient (NAG)**
- **Looks ahead** before updating weights, improving convergence speed.  

#### **Syntax**
```python
tf.keras.optimizers.SGD(learning_rate=0.01, momentum=0.9, nesterov=True)
```

#### **Example**
```python
optimizer = tf.keras.optimizers.SGD(learning_rate=0.01, momentum=0.9, nesterov=True)
```

---

### **4. Adagrad**
- **Adapts learning rate** for each parameter, making large updates for infrequent features.  
- **Not good for deep learning** (learning rate decreases over time).  

#### **Syntax**
```python
tf.keras.optimizers.Adagrad(learning_rate=0.01)
```

#### **Example**
```python
optimizer = tf.keras.optimizers.Adagrad(learning_rate=0.01)
```

---

### **5. RMSprop**
- Keeps a **moving average of squared gradients**, preventing learning rate decay.  
- **Preferred for RNNs**.  

#### **Syntax**
```python
tf.keras.optimizers.RMSprop(learning_rate=0.001, rho=0.9)
```

#### **Example**
```python
optimizer = tf.keras.optimizers.RMSprop(learning_rate=0.001, rho=0.9)
```

---

### **6. Adam (Adaptive Moment Estimation)**
- **Combines Momentum and RMSprop**, making it widely used.  
- **Default optimizer for deep learning**.  

#### **Syntax**
```python
tf.keras.optimizers.Adam(learning_rate=0.001, beta_1=0.9, beta_2=0.999)
```

#### **Example**
```python
optimizer = tf.keras.optimizers.Adam(learning_rate=0.001, beta_1=0.9, beta_2=0.999)
```

---

### **7. AdaMax**
- **Variant of Adam** using infinity norm, making it more stable.  

#### **Syntax**
```python
tf.keras.optimizers.Adamax(learning_rate=0.002)
```

#### **Example**
```python
optimizer = tf.keras.optimizers.Adamax(learning_rate=0.002)
```

---

### **8. Nadam (Nesterov-accelerated Adaptive Moment Estimation)**
- Combines **Adam and Nesterov momentum**, leading to faster convergence.  

#### **Syntax**
```python
tf.keras.optimizers.Nadam(learning_rate=0.002)
```

#### **Example**
```python
optimizer = tf.keras.optimizers.Nadam(learning_rate=0.002)
```

---

### **9. FTRL (Follow The Regularized Leader)**
- Used for **linear models**, applying **L1 and L2 regularization**.  

#### **Syntax**
```python
tf.keras.optimizers.Ftrl(learning_rate=0.01)
```

#### **Example**
```python
optimizer = tf.keras.optimizers.Ftrl(learning_rate=0.01)
```

---

### **Comparison of Optimizers**

| **Optimizer** | **Best Used For** | **Speed** | **Memory Usage** | **Convergence Stability** |
|--------------|------------------|-----------|------------------|----------------------|
| **SGD** | General optimization | Slow | Low | Low |
| **Momentum** | Faster SGD | Medium | Low | Medium |
| **NAG** | Faster Momentum | Fast | Low | High |
| **Adagrad** | NLP, Sparse Data | Medium | High | Medium |
| **RMSprop** | RNNs, Non-stationary Data | Fast | Medium | High |
| **Adam** | Most DL tasks | Fast | Medium | Very High |
| **AdaMax** | Stable Adam variant | Fast | Medium | High |
| **Nadam** | Faster Adam | Very Fast | Medium | High |
| **FTRL** | Large-scale models | Medium | Low | Medium |

---

### **Conclusion**
- **SGD and Momentum** are basic optimizers but slow for deep learning.  
- **Adam, RMSprop, and Nadam** are best for deep learning tasks.  
- **Adagrad and FTRL** are used for sparse data and linear models.  
- **Choosing the right optimizer** affects model accuracy and speed.