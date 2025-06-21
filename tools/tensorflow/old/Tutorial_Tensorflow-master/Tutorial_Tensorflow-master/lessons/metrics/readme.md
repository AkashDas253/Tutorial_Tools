## **Metrics in TensorFlow**  

### **Overview**  
Metrics evaluate a model’s performance by measuring how well predictions match actual values. In TensorFlow, `tf.keras.metrics` provides built-in metrics for classification, regression, and other tasks.

---

### **Types of Metrics**  

| **Category** | **Metric** | **Formula / Definition** | **Usage in TensorFlow** |
|-------------|-----------|-------------------------|-------------------------|
| **Regression** | Mean Squared Error (MSE) | \( \frac{1}{N} \sum (y - \hat{y})^2 \) | `tf.keras.metrics.MeanSquaredError()` |
| | Mean Absolute Error (MAE) | \( \frac{1}{N} \sum |y - \hat{y}| \) | `tf.keras.metrics.MeanAbsoluteError()` |
| | Mean Absolute Percentage Error (MAPE) | \( \frac{100}{N} \sum \left| \frac{y - \hat{y}}{y} \right| \) | `tf.keras.metrics.MeanAbsolutePercentageError()` |
| | Mean Squared Logarithmic Error (MSLE) | \( \frac{1}{N} \sum (\log(y+1) - \log(\hat{y}+1))^2 \) | `tf.keras.metrics.MeanSquaredLogarithmicError()` |
| **Classification** | Accuracy | \( \frac{\text{correct predictions}}{\text{total predictions}} \) | `tf.keras.metrics.Accuracy()` |
| | Binary Accuracy | Used for binary classification | `tf.keras.metrics.BinaryAccuracy()` |
| | Categorical Accuracy | Used for multi-class classification | `tf.keras.metrics.CategoricalAccuracy()` |
| | Top-K Categorical Accuracy | Measures if true label is in the top-K predictions | `tf.keras.metrics.TopKCategoricalAccuracy(k=5)` |
| | Precision | \( \frac{\text{TP}}{\text{TP + FP}} \) | `tf.keras.metrics.Precision()` |
| | Recall (Sensitivity) | \( \frac{\text{TP}}{\text{TP + FN}} \) | `tf.keras.metrics.Recall()` |
| | F1 Score | \( 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}} \) | Custom implementation |
| **Probabilistic** | AUC (Area Under Curve) | Measures classifier quality via ROC curve | `tf.keras.metrics.AUC()` |
| | Log Loss (Cross-Entropy) | Measures difference between true labels and predicted probabilities | `tf.keras.metrics.BinaryCrossentropy()` |
| **Ranking** | Mean Reciprocal Rank (MRR) | Used in recommendation systems | `tf.keras.metrics.Mean()` (custom implementation) |

---

### **1. Regression Metrics**
#### **Mean Squared Error (MSE)**
- Penalizes large errors more than small ones.  
- Used when **large errors should be minimized**.  

#### **Syntax**
```python
tf.keras.metrics.MeanSquaredError()
```

#### **Example**
```python
mse = tf.keras.metrics.MeanSquaredError()
mse.update_state([3, 5, 2], [2.5, 5.2, 1.8])
print(mse.result().numpy())  # Output: MSE value
```

---

#### **Mean Absolute Error (MAE)**
- Measures average absolute difference between actual and predicted values.  
- Less sensitive to **outliers** than MSE.  

#### **Syntax**
```python
tf.keras.metrics.MeanAbsoluteError()
```

#### **Example**
```python
mae = tf.keras.metrics.MeanAbsoluteError()
mae.update_state([3, 5, 2], [2.5, 5.2, 1.8])
print(mae.result().numpy())  # Output: MAE value
```

---

### **2. Classification Metrics**
#### **Accuracy**
- Measures **overall correctness** of predictions.  
- Works well when **classes are balanced**.  

#### **Syntax**
```python
tf.keras.metrics.Accuracy()
```

#### **Example**
```python
accuracy = tf.keras.metrics.Accuracy()
accuracy.update_state([1, 0, 1, 1], [1, 0, 0, 1])
print(accuracy.result().numpy())  # Output: Accuracy value
```

---

#### **Binary Accuracy**
- Used for **binary classification** tasks.  

#### **Syntax**
```python
tf.keras.metrics.BinaryAccuracy()
```

#### **Example**
```python
binary_acc = tf.keras.metrics.BinaryAccuracy()
binary_acc.update_state([1, 0, 1, 1], [0.9, 0.3, 0.8, 0.6])
print(binary_acc.result().numpy())  # Output: Binary Accuracy
```

---

#### **Categorical Accuracy**
- Used for **multi-class classification**.  

#### **Syntax**
```python
tf.keras.metrics.CategoricalAccuracy()
```

#### **Example**
```python
cat_acc = tf.keras.metrics.CategoricalAccuracy()
cat_acc.update_state([[0, 0, 1], [0, 1, 0]], [[0, 0, 1], [0, 1, 0]])
print(cat_acc.result().numpy())  # Output: Categorical Accuracy
```

---

#### **Precision & Recall**
| **Metric** | **Meaning** | **Best for** |
|-----------|------------|--------------|
| **Precision** | Measures how many predicted positives are actually correct. | Avoiding **false positives** (e.g., spam detection) |
| **Recall** | Measures how many actual positives were correctly identified. | Avoiding **false negatives** (e.g., medical diagnosis) |

#### **Syntax**
```python
tf.keras.metrics.Precision()
tf.keras.metrics.Recall()
```

#### **Example**
```python
precision = tf.keras.metrics.Precision()
precision.update_state([1, 0, 1, 1], [1, 0, 0, 1])
print(precision.result().numpy())  # Output: Precision

recall = tf.keras.metrics.Recall()
recall.update_state([1, 0, 1, 1], [1, 0, 0, 1])
print(recall.result().numpy())  # Output: Recall
```

---

#### **F1 Score (Custom Implementation)**
- Harmonic mean of **Precision and Recall**.  

#### **Example**
```python
precision = tf.keras.metrics.Precision()
recall = tf.keras.metrics.Recall()

precision.update_state([1, 0, 1, 1], [1, 0, 0, 1])
recall.update_state([1, 0, 1, 1], [1, 0, 0, 1])

f1_score = 2 * (precision.result().numpy() * recall.result().numpy()) / (precision.result().numpy() + recall.result().numpy())
print(f1_score)  # Output: F1 Score
```

---

### **3. Probabilistic Metrics**
#### **AUC (Area Under Curve)**
- Measures **discrimination** between positive and negative classes.  
- Higher AUC = better model performance.  

#### **Syntax**
```python
tf.keras.metrics.AUC()
```

#### **Example**
```python
auc = tf.keras.metrics.AUC()
auc.update_state([1, 0, 1, 1], [0.9, 0.3, 0.8, 0.6])
print(auc.result().numpy())  # Output: AUC Score
```

---

### **Comparison of Metrics**
| **Metric** | **Best Used For** | **Sensitivity to Class Imbalance** |
|-----------|------------------|----------------------------------|
| **Accuracy** | General classification | High (misleading if classes are imbalanced) |
| **Precision** | Reducing false positives | Less sensitive |
| **Recall** | Reducing false negatives | More sensitive |
| **F1 Score** | Balanced measure of precision & recall | Medium sensitivity |
| **AUC** | Measuring classifier performance | Robust against imbalance |

---

### **Conclusion**
- **Regression tasks** use **MSE, MAE, MAPE, MSLE**.  
- **Classification tasks** use **Accuracy, Precision, Recall, and F1 Score**.  
- **AUC and Log Loss** are used for **probabilistic models**.  
- **Choosing the right metric** is **crucial** for performance evaluation.