## **Model Compilation in TensorFlow**  

### **Overview**  
Model compilation in TensorFlow defines how a model learns by specifying:  
- **Loss function** (to measure errors)  
- **Optimizer** (to update weights)  
- **Metrics** (to evaluate performance)  

Before training, a model must be compiled using `model.compile()` in **Keras**.  

---

### **1. Syntax**  
```python
model.compile(optimizer='adam', loss='sparse_categorical_crossentropy', metrics=['accuracy'])
```
- **`optimizer`**: Controls learning by adjusting weights.  
- **`loss`**: Determines how well the model performs.  
- **`metrics`**: Evaluates performance (e.g., `accuracy`).  

---

### **2. Parameters in `model.compile()`**  

| **Parameter** | **Purpose** | **Examples** |
|--------------|------------|-------------|
| **`optimizer`** | Updates weights to minimize loss. | `'adam'`, `'sgd'`, `'rmsprop'`, `tf.keras.optimizers.Adam(learning_rate=0.001)` |
| **`loss`** | Computes error between predicted and actual values. | `'mse'`, `'binary_crossentropy'`, `'categorical_crossentropy'` |
| **`metrics`** | Tracks model performance. | `['accuracy']`, `['precision', 'recall']` |

---

### **3. Optimizers**  
| **Optimizer** | **Usage** |
|-------------|----------|
| `sgd` | Simple Stochastic Gradient Descent |
| `adam` | Adaptive learning, commonly used |
| `rmsprop` | Works well for recurrent networks |
| `adagrad` | Adjusts learning rate per feature |

#### **Example**  
```python
model.compile(optimizer=tf.keras.optimizers.Adam(learning_rate=0.001),
              loss='categorical_crossentropy',
              metrics=['accuracy'])
```

---

### **4. Loss Functions**  
| **Loss Type** | **Loss Function** | **Use Case** |
|-------------|---------------|----------|
| **Regression** | `mse` (Mean Squared Error) | Continuous values |
|  | `mae` (Mean Absolute Error) | Outlier-sensitive regression |
| **Classification** | `binary_crossentropy` | Binary classification |
|  | `categorical_crossentropy` | Multi-class (one-hot encoded) |
|  | `sparse_categorical_crossentropy` | Multi-class (integer labels) |

#### **Example**  
```python
model.compile(optimizer='adam', loss='sparse_categorical_crossentropy', metrics=['accuracy'])
```

---

### **5. Metrics**  
| **Metric** | **Purpose** |
|-----------|----------|
| `accuracy` | Measures correct predictions |
| `precision` | Measures true positive rate |
| `recall` | Measures true positive coverage |
| `AUC` | Area under ROC curve |

#### **Example**  
```python
model.compile(optimizer='adam', loss='binary_crossentropy', metrics=['accuracy', 'AUC'])
```

---

### **6. Custom Loss & Metrics**  
#### **Custom Loss Example**  
```python
def custom_loss(y_true, y_pred):
    return tf.reduce_mean(tf.square(y_true - y_pred))  # MSE

model.compile(optimizer='adam', loss=custom_loss, metrics=['mae'])
```

#### **Custom Metric Example**  
```python
import tensorflow.keras.backend as K

def f1_score(y_true, y_pred):
    precision = K.sum(K.round(y_pred) * y_true) / (K.sum(K.round(y_pred)) + K.epsilon())
    recall = K.sum(K.round(y_pred) * y_true) / (K.sum(y_true) + K.epsilon())
    return 2 * (precision * recall) / (precision + recall + K.epsilon())

model.compile(optimizer='adam', loss='binary_crossentropy', metrics=[f1_score])
```

---

### **7. Example: Compiling a Model**  
```python
import tensorflow as tf
from tensorflow import keras

model = keras.Sequential([
    keras.layers.Dense(128, activation='relu'),
    keras.layers.Dense(10, activation='softmax')
])

model.compile(optimizer='adam', loss='sparse_categorical_crossentropy', metrics=['accuracy'])
```

---

### **Conclusion**
- **Compilation** is required before training.  
- **Optimizer**, **loss function**, and **metrics** must be chosen based on the problem type.  
- **Custom loss functions and metrics** allow more flexibility.