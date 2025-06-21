## **Constants in TensorFlow**  

### **Overview**  
In TensorFlow, **constants** are immutable tensors whose values do not change during execution. They are created using `tf.constant()` and are useful for defining fixed values in a computational graph.  

---

## **1. Creating Constants**  

| **Method** | **Description** | **Example** |
|-----------|---------------|-------------|
| **Scalar Constant** | A single fixed value. | `tf.constant(5.0)` |
| **Vector Constant** | A 1D array of fixed values. | `tf.constant([1, 2, 3])` |
| **Matrix Constant** | A 2D array (or higher) of fixed values. | `tf.constant([[1, 2], [3, 4]])` |
| **Data Type Specification** | Explicitly defining the tensor type. | `tf.constant(3, dtype=tf.float32)` |

---

## **2. Examples**  

### **A. Creating a Scalar Constant**  
```python
import tensorflow as tf

x = tf.constant(5.0)
print(x)
```

### **B. Creating a Vector Constant**  
```python
v = tf.constant([1, 2, 3], dtype=tf.int32)
print(v)
```

### **C. Creating a Matrix Constant**  
```python
m = tf.constant([[1, 2], [3, 4]], dtype=tf.float32)
print(m)
```

---

## **3. Properties of Constants**  

| **Property** | **Description** |
|-------------|----------------|
| **Immutable** | Cannot be changed after creation. |
| **Efficient** | Stored in memory for fast access. |
| **Supports Various Data Types** | Includes `int32`, `float32`, `bool`, `string`, etc. |
| **Can Be Used in Operations** | Can be added, multiplied, or used in computations. |

---

## **4. Using Constants in Operations**  
```python
a = tf.constant(3)
b = tf.constant(4)
c = a + b  # TensorFlow automatically computes the result
print(c)
```

---

## **5. Differences Between Constants and Variables**  

| **Feature** | **tf.constant()** | **tf.Variable()** |
|------------|-----------------|-----------------|
| **Mutability** | Immutable | Mutable |
| **Usage** | Fixed values | Trainable parameters |
| **Memory Allocation** | Stored once | Updated during training |

---

## **6. Summary**  
- `tf.constant()` creates **immutable** tensors.  
- Supports **scalars, vectors, matrices**, and various **data types**.  
- Used for **fixed values** in computations.  
- **Cannot be updated**, unlike `tf.Variable()`.