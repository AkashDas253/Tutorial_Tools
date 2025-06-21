## **TensorFlow Operations**  

### **Overview**  
Operations (`ops`) in TensorFlow perform computations on tensors, including arithmetic, linear algebra, transformations, and reductions.

---

### **Basic Arithmetic Operations**  

| **Operation**  | **Description**            | **Example**                          |
|--------------|--------------------|----------------------------------|
| Addition     | Element-wise sum   | `tf.add(a, b)` or `a + b`       |
| Subtraction  | Element-wise diff  | `tf.subtract(a, b)` or `a - b`  |
| Multiplication | Element-wise product | `tf.multiply(a, b)` or `a * b`  |
| Division     | Element-wise division | `tf.divide(a, b)` or `a / b`    |
| Power       | Element-wise exponentiation | `tf.pow(a, b)` or `a ** b`      |
| Modulus     | Element-wise remainder | `tf.math.mod(a, b)`             |
| Absolute    | Element-wise absolute value | `tf.abs(a)`                    |

---

### **Linear Algebra Operations**  

| **Operation**     | **Description**                      | **Example**                         |
|------------------|----------------------------------|--------------------------------|
| Matrix Multiplication | Dot product              | `tf.matmul(a, b)`             |
| Transpose        | Swaps rows and columns        | `tf.transpose(a)`             |
| Inverse          | Computes matrix inverse      | `tf.linalg.inv(a)`            |
| Determinant      | Computes determinant        | `tf.linalg.det(a)`            |
| Eigenvalues      | Computes eigenvalues        | `tf.linalg.eigvals(a)`        |
| QR Decomposition | Computes QR factorization  | `tf.linalg.qr(a)`             |

---

### **Reduction Operations**  

| **Operation**    | **Description**                       | **Example**                        |
|-----------------|-----------------------------------|--------------------------------|
| Sum            | Computes total sum               | `tf.reduce_sum(a)`            |
| Mean           | Computes average                 | `tf.reduce_mean(a)`           |
| Min            | Finds minimum value              | `tf.reduce_min(a)`            |
| Max            | Finds maximum value              | `tf.reduce_max(a)`            |
| Argmin         | Index of minimum value          | `tf.argmin(a)`                |
| Argmax         | Index of maximum value          | `tf.argmax(a)`                |
| Standard Deviation | Computes standard deviation | `tf.math.reduce_std(a)`       |

---

### **Logical Operations**  

| **Operation**  | **Description**                     | **Example**                         |
|--------------|-----------------------------|--------------------------------|
| Greater     | Element-wise comparison (`>`)| `tf.greater(a, b)`             |
| Less        | Element-wise comparison (`<`)| `tf.less(a, b)`                |
| Equal       | Checks equality (`==`)      | `tf.equal(a, b)`               |
| Not Equal   | Checks inequality (`!=`)    | `tf.not_equal(a, b)`           |
| Logical AND | Element-wise AND operation  | `tf.logical_and(a, b)`         |
| Logical OR  | Element-wise OR operation   | `tf.logical_or(a, b)`          |

---

### **Trigonometric Operations**  

| **Operation** | **Description**          | **Example**                 |
|-------------|----------------|------------------------|
| Sine        | Computes sine   | `tf.sin(a)`           |
| Cosine      | Computes cosine | `tf.cos(a)`           |
| Tangent     | Computes tangent | `tf.tan(a)`           |
| Arc Sine    | Inverse sine     | `tf.asin(a)`          |
| Arc Cosine  | Inverse cosine   | `tf.acos(a)`          |
| Arc Tangent | Inverse tangent  | `tf.atan(a)`          |

---

### **Exponential and Logarithmic Operations**  

| **Operation**  | **Description**                 | **Example**                   |
|--------------|-----------------------|----------------------|
| Exponential  | Computes `e^x`        | `tf.exp(a)`         |
| Logarithm    | Natural log (`ln(x)`) | `tf.math.log(a)`    |
| Log10        | Log base 10            | `tf.math.log(a) / tf.math.log(10.0)` |

---

### **Tensor Reshaping Operations**  

| **Operation**   | **Description**                           | **Example**                        |
|---------------|-----------------------------------|--------------------------------|
| Reshape      | Changes tensor shape             | `tf.reshape(a, [2, 3])`       |
| Expand Dims  | Adds a new dimension             | `tf.expand_dims(a, axis=0)`   |
| Squeeze      | Removes single dimensions       | `tf.squeeze(a)`               |
| Concatenate  | Merges tensors along an axis    | `tf.concat([a, b], axis=0)`   |
| Stack        | Stacks tensors along a new axis | `tf.stack([a, b], axis=1)`    |

---

### **Broadcasting Operations**  

| **Operation**        | **Shape A** | **Shape B** | **Result Shape** |
|--------------------|------------|------------|----------------|
| `[3, 3] + [3]`    | `(3, 3)`    | `(3,)`     | `(3, 3)`       |
| `[3, 3] + [1, 3]` | `(3, 3)`    | `(1, 3)`   | `(3, 3)`       |

---

### **Gradient Computation**  

| **Operation**  | **Description**                               | **Example**                          |
|--------------|-----------------------------------|--------------------------------|
| Compute Gradient | Computes derivative using auto-diff | `tape.gradient(y, x)`        |
| Hessian Matrix  | Second-order derivative matrix | `tf.hessians(y, x)`           |

---

### **Special Operations**  

| **Operation**       | **Description**                      | **Example**                          |
|-------------------|--------------------------------|--------------------------------|
| One-Hot Encoding | Converts indices to one-hot vectors | `tf.one_hot([0,1,2], depth=3)` |
| Sorting         | Sorts tensor elements              | `tf.sort(tensor)`              |
| Argmax         | Finds index of maximum value      | `tf.argmax(tensor)`            |
| Element-wise Max | Finds max values element-wise     | `tf.maximum(a, b)`             |

---

### **Conclusion**  
TensorFlow operations enable various computations on tensors, from basic arithmetic to linear algebra, reshaping, and automatic differentiation. These operations are optimized for both CPU and GPU execution.