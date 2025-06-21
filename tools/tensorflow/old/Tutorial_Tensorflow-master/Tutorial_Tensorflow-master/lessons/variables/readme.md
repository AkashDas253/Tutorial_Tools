## **TensorFlow Variables**  

### **Overview**  
A TensorFlow `Variable` is a special type of tensor that can be updated during training. Unlike `tf.constant`, which is immutable, `tf.Variable` allows modifications.

---

### **Creating Variables**  

| **Method**             | **Description**                          | **Example**                      |
|----------------------|----------------------------------|--------------------------------|
| `tf.Variable`       | Creates a variable with initial values | `tf.Variable([1, 2, 3])`      |
| `tf.zeros`          | Variable initialized with zeros    | `tf.Variable(tf.zeros([3,3]))` |
| `tf.ones`           | Variable initialized with ones     | `tf.Variable(tf.ones([2,2]))`  |
| `tf.random.normal`  | Random normal values              | `tf.Variable(tf.random.normal([2,3]))` |

---

### **Variable Attributes**  

| **Attribute**        | **Description**                              | **Example**                          |
|----------------------|----------------------------------|--------------------------------|
| `shape`             | Returns the shape of the variable | `var.shape`                    |
| `dtype`             | Data type of the variable        | `var.dtype`                    |
| `name`              | Name assigned to the variable    | `var.name`                     |
| `trainable`         | Whether the variable is trainable | `var.trainable`                |

---

### **Updating Variable Values**  

| **Operation**       | **Description**                          | **Example**                      |
|--------------------|----------------------------------|--------------------------------|
| Assign a new value | Changes variable's value      | `var.assign([4, 5, 6])`       |
| Add to variable   | Element-wise addition         | `var.assign_add([1, 1, 1])`   |
| Subtract from variable | Element-wise subtraction  | `var.assign_sub([1, 1, 1])`   |

---

### **Variable vs. Tensor**  

| **Feature**        | **`tf.Variable`**                 | **`tf.Tensor`**                |
|-------------------|--------------------------------|--------------------------------|
| Mutability       | Mutable (can be updated)       | Immutable (fixed value)        |
| Used in training | Yes (weights, biases, etc.)    | Mostly for computation         |
| Requires `assign` | Yes (`assign()`, `assign_add()`) | No (direct arithmetic works)   |

---

### **Trainable Variables**  

Variables marked as **trainable** are automatically tracked for optimization.  

#### **Example**:  
```python
var = tf.Variable(3.0, trainable=True)
```

To get all trainable variables:  
```python
tf.trainable_variables()
```

---

### **Using Variables in Models**  

Variables are commonly used for storing **weights** and **biases** in models.  

#### **Example**:  
```python
W = tf.Variable(tf.random.normal([3,3]), name="weights")
b = tf.Variable(tf.zeros([3]), name="bias")
```

---

### **Variable Persistence (Saving & Loading)**  

| **Operation**    | **Command**                                      |
|-----------------|------------------------------------------------|
| Save Model Variables | `tf.train.Checkpoint(model).save(filepath)` |
| Load Variables | `tf.train.Checkpoint(model).restore(filepath)` |

---

### **Conclusion**  
TensorFlow Variables are mutable tensors used in machine learning models to store trainable parameters like weights and biases. They support various operations and can be updated dynamically during training.