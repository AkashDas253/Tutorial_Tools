## **Loss Functions in TensorFlow**  

### **Overview**  
Loss functions measure the **difference between predicted** and **actual values**, guiding the **optimization process** in deep learning. The choice of loss function depends on the **task type**, such as **classification, regression, or specialized problems**.

---

### **Types of Loss Functions**  

| **Category** | **Loss Function** | **Formula** | **Usage** | **Example in TensorFlow** |
|-------------|------------------|------------|------------|---------------------------|
| **Regression** | Mean Squared Error (MSE) | \( \frac{1}{N} \sum (y_i - \hat{y}_i)^2 \) | Continuous value prediction | `tf.keras.losses.MeanSquaredError()` |
| | Mean Absolute Error (MAE) | \( \frac{1}{N} \sum |y_i - \hat{y}_i| \) | Less sensitive to outliers than MSE | `tf.keras.losses.MeanAbsoluteError()` |
| | Huber Loss | \(\begin{cases} \frac{1}{2} (y - \hat{y})^2 & \text{if } |y - \hat{y}| \leq \delta \\ \delta (|y - \hat{y}| - \frac{1}{2} \delta) & \text{otherwise} \end{cases}\) | Robust against outliers | `tf.keras.losses.Huber(delta=1.0)` |
| | Log-Cosh Loss | \( \sum \log(\cosh(y - \hat{y})) \) | Similar to MSE but smooth for large errors | `tf.keras.losses.LogCosh()` |
| **Classification** | Binary Cross-Entropy | \( -\frac{1}{N} \sum \big(y \log(\hat{y}) + (1 - y) \log(1 - \hat{y})\big) \) | Binary classification | `tf.keras.losses.BinaryCrossentropy()` |
| | Categorical Cross-Entropy | \( -\sum y_i \log(\hat{y}_i) \) | Multi-class classification (one-hot labels) | `tf.keras.losses.CategoricalCrossentropy()` |
| | Sparse Categorical Cross-Entropy | \( -\sum y_i \log(\hat{y}_i) \) | Multi-class classification (integer labels) | `tf.keras.losses.SparseCategoricalCrossentropy()` |
| **Ranking & Custom Losses** | Hinge Loss | \( \sum \max(0, 1 - y \cdot \hat{y}) \) | Used in SVMs for classification | `tf.keras.losses.Hinge()` |
| | Kullback-Leibler Divergence (KL Divergence) | \( \sum y_i \log(\frac{y_i}{\hat{y}_i}) \) | Measures probability distribution difference | `tf.keras.losses.KLDivergence()` |
| | Custom Loss | Defined by the user | Specialized use cases | Custom function |

---

### **1. Mean Squared Error (MSE)**
- Measures **average squared difference** between actual and predicted values.  
- **Sensitive to outliers** due to squaring.  

#### **Syntax**
```python
tf.keras.losses.MeanSquaredError()
```

#### **Example**
```python
mse_loss = tf.keras.losses.MeanSquaredError()
loss_value = mse_loss(y_true, y_pred)
```

---

### **2. Mean Absolute Error (MAE)**
- Computes the **absolute difference** instead of squaring errors.  
- **Less sensitive to outliers** than MSE.  

#### **Syntax**
```python
tf.keras.losses.MeanAbsoluteError()
```

#### **Example**
```python
mae_loss = tf.keras.losses.MeanAbsoluteError()
loss_value = mae_loss(y_true, y_pred)
```

---

### **3. Huber Loss**
- Combines **MSE** and **MAE**, being **robust to outliers**.  

#### **Syntax**
```python
tf.keras.losses.Huber(delta=1.0)
```

#### **Example**
```python
huber_loss = tf.keras.losses.Huber(delta=1.0)
loss_value = huber_loss(y_true, y_pred)
```

---

### **4. Binary Cross-Entropy**
- Used for **binary classification problems**.  

#### **Syntax**
```python
tf.keras.losses.BinaryCrossentropy()
```

#### **Example**
```python
bce_loss = tf.keras.losses.BinaryCrossentropy()
loss_value = bce_loss(y_true, y_pred)
```

---

### **5. Categorical Cross-Entropy**
- Used for **multi-class classification** with **one-hot labels**.  

#### **Syntax**
```python
tf.keras.losses.CategoricalCrossentropy()
```

#### **Example**
```python
cce_loss = tf.keras.losses.CategoricalCrossentropy()
loss_value = cce_loss(y_true, y_pred)
```

---

### **6. Sparse Categorical Cross-Entropy**
- Used for **multi-class classification** with **integer labels**.  

#### **Syntax**
```python
tf.keras.losses.SparseCategoricalCrossentropy()
```

#### **Example**
```python
scce_loss = tf.keras.losses.SparseCategoricalCrossentropy()
loss_value = scce_loss(y_true, y_pred)
```

---

### **7. Custom Loss Function**
- Allows defining **problem-specific** loss.  

#### **Example**
```python
def custom_loss(y_true, y_pred):
    return tf.reduce_mean(tf.square(y_true - y_pred))

model.compile(optimizer='adam', loss=custom_loss)
```

---

### **Comparison of Loss Functions**

| **Loss Function** | **Best Used For** | **Outlier Sensitivity** | **Computational Cost** |
|------------------|------------------|------------------|------------------|
| **MSE** | Regression | High | Low |
| **MAE** | Regression | Medium | Low |
| **Huber** | Regression with Outliers | Low | Medium |
| **Log-Cosh** | Regression | Low | High |
| **Binary Cross-Entropy** | Binary Classification | Medium | Medium |
| **Categorical Cross-Entropy** | Multi-Class (One-Hot) | Medium | Medium |
| **Sparse Categorical Cross-Entropy** | Multi-Class (Integer Labels) | Medium | Medium |
| **Hinge Loss** | SVM Classification | Low | Medium |
| **KL Divergence** | Probability Distributions | High | High |

---

### **Conclusion**
- **MSE** and **MAE** are used for **regression**, with **Huber** better for **outliers**.  
- **Cross-Entropy** is best for **classification**, with **Binary Cross-Entropy** for **binary tasks**.  
- **KL Divergence** and **Hinge Loss** serve specialized use cases.  
- **Custom losses** allow fine-tuning based on problem needs.