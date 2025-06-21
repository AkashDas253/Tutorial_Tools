## Tensors

---

### **Tensor Creation**
- **Basic Tensor Creation**:
  - `tf.constant()`
  - `tf.Variable()`
  - `tf.zeros()`
  - `tf.ones()`
  - `tf.fill()`
  - `tf.eye()`
  - `tf.random.normal()`
  - `tf.random.uniform()`
  - `tf.range()`
- **Tensor from NumPy**:
  - `tf.convert_to_tensor()`
  - `tf.make_tensor_proto()`

### **Tensor Operations**
- **Arithmetic Operations**:
  - Addition: `tf.add()`, `+`
  - Subtraction: `tf.subtract()`, `-`
  - Multiplication: `tf.multiply()`, `*`
  - Division: `tf.divide()`, `/`
  - Exponentiation: `tf.pow()`
  - Modulo: `tf.math.mod()`
  - Floor Division: `tf.math.floordiv()`
  - Square Root: `tf.sqrt()`
  - Absolute: `tf.abs()`
  - Minimum/Maximum: `tf.minimum()`, `tf.maximum()`
- **Matrix Operations**:
  - Matrix Multiplication: `tf.matmul()`
  - Transpose: `tf.transpose()`
  - Determinant: `tf.linalg.det()`
  - Inverse: `tf.linalg.inv()`
  - Eigenvalues: `tf.linalg.eigvals()`
- **Reduction Operations**:
  - Sum: `tf.reduce_sum()`
  - Mean: `tf.reduce_mean()`
  - Maximum/Minimum: `tf.reduce_max()`, `tf.reduce_min()`
  - Product: `tf.reduce_prod()`
  - Logical Operations: `tf.reduce_all()`, `tf.reduce_any()`
- **Comparison Operations**:
  - Equal: `tf.equal()`
  - Greater/Less: `tf.greater()`, `tf.less()`
  - Logical And/Or: `tf.logical_and()`, `tf.logical_or()`

### **Reshaping and Slicing**
- **Reshaping**:
  - `tf.reshape()`
  - `tf.expand_dims()`
  - `tf.squeeze()`
- **Slicing and Indexing**:
  - `tf.gather()`
  - `tf.boolean_mask()`
  - `tf.slice()`
  - `tf.strided_slice()`
  - `tf.take()`

### **Broadcasting**
- **Broadcasting Rules**:
  - Implicit broadcasting for tensors with different shapes.
  - `tf.broadcast_static_shape()`
  - `tf.broadcast_to()`

### **Tensor Attributes**
- **Shape and Size**:
  - `tf.shape()`
  - `tf.rank()`
  - `tf.size()`
- **Tensor Data Types**:
  - `tf.dtypes.as_dtype()`
  - `tf.cast()`
  - Checking Tensor Types: `tf.dtypes.is_integer()`, `tf.dtypes.is_floating()`

### **Tensor Functions (Utility and Miscellaneous)**
- **Checking Tensor Type**:
  - `tf.is_tensor()`
  - `tf.stop_gradient()`
  - `tf.identity()`
- **Tensor Conversion and Creation**:
  - `tf.convert_to_tensor()`
  - `tf.make_tensor_proto()`
- **Debugging and Assertions**:
  - `tf.debugging.assert_rank()`
  - `tf.debugging.assert_non_negative()`
  - `tf.debugging.check_numerics()`

### **Tensor Algebra and Linear Algebra**
- **Linear Algebra Functions**:
  - Norms: `tf.linalg.norm()`
  - Eigenvalues: `tf.linalg.eigvals()`
  - Matrix Inverse: `tf.linalg.inv()`
  - Matrix Determinant: `tf.linalg.det()`
  - Singular Value Decomposition (SVD): `tf.linalg.svd()`
  - QR Decomposition: `tf.linalg.qr()`
  - Eigen Decomposition: `tf.linalg.eigh()`

### **Tensor Aggregation**
- **Aggregation Operations**:
  - Sum: `tf.reduce_sum()`
  - Mean: `tf.reduce_mean()`
  - Maximum/Minimum: `tf.reduce_max()`, `tf.reduce_min()`
  - Product: `tf.reduce_prod()`
  - Logical: `tf.reduce_all()`, `tf.reduce_any()`

### **Tensor Indexing, Slicing, and Masking**
- **Indexing and Slicing**:
  - `tf.gather()`
  - `tf.boolean_mask()`
  - `tf.slice()`
  - `tf.strided_slice()`
- **Masking**:
  - `tf.boolean_mask()`

### **Other Tensor Functions**
- **Mathematical Functions**:
  - `tf.math.sqrt()`, `tf.math.log()`, `tf.math.exp()`
  - `tf.math.sin()`, `tf.math.cos()`
- **Logical and Comparison Operations**:
  - `tf.equal()`, `tf.not_equal()`
  - `tf.greater()`, `tf.less()`
  - `tf.logical_and()`, `tf.logical_or()`
- **Tensor Utility Functions**:
  - `tf.is_tensor()`
  - `tf.convert_to_tensor()`
  - `tf.identity()`

---

### **Advanced Tensor Operations**
- **TensorFlow Graph Functions**:
  - `tf.function()`
  - `tf.autodiff`
- **TensorFlow Dataset API**:
  - `tf.data.Dataset`
  - `tf.data.from_tensor_slices()`

---

### **1. Tensor Creation Functions**

| Function           | Parameters                                                                 | Description                                                                                           | Example                                                                                      |
|--------------------|---------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|
| `tf.constant`      | `value, dtype=None, shape=None, name='Const'`                              | Creates a constant tensor. <br> - `value`: Value of the elements in the tensor. <br> - `dtype`: (Optional) Data type of the tensor. <br> - `shape`: (Optional) Shape of the tensor. <br> - `name`: (Optional) Name of the tensor. | `tf.constant([1, 2, 3], dtype=tf.float32)`                                                  |
| `tf.zeros`         | `shape, dtype=tf.float32, name=None`                                       | Creates a tensor with all elements set to zero. <br> - `shape`: Shape of the tensor. <br> - `dtype`: (Optional) Data type of the tensor. <br> - `name`: (Optional) Name of the tensor. | `tf.zeros([2, 3])`                                                                          |
| `tf.ones`          | `shape, dtype=tf.float32, name=None`                                       | Creates a tensor with all elements set to one. <br> - `shape`: Shape of the tensor. <br> - `dtype`: (Optional) Data type of the tensor. <br> - `name`: (Optional) Name of the tensor. | `tf.ones([2, 3])`                                                                           |
| `tf.fill`          | `dims, value, name=None`                                                   | Creates a tensor filled with a scalar value. <br> - `dims`: Shape of the tensor. <br> - `value`: Scalar value to fill the tensor with. <br> - `name`: (Optional) Name of the tensor. | `tf.fill([2, 3], 5)`                                                                        |
| `tf.eye`           | `num_rows, num_columns=None, batch_shape=None, dtype=tf.float32, name=None` | Creates a tensor with ones on the diagonal and zeros elsewhere (identity matrix). <br> - `num_rows`: Number of rows. <br> - `num_columns`: (Optional) Number of columns (defaults to square matrix). <br> - `batch_shape`: (Optional) Shape for a batch of identity matrices. | `tf.eye(3)`                                                                                 |
| `tf.linspace`      | `start, stop, num, dtype=tf.float32, name=None`                             | Generates `num` evenly spaced values between `start` and `stop`. <br> - `start`: Starting value. <br> - `stop`: Ending value. <br> - `num`: Number of values. <br> - `dtype`: (Optional) Data type of the values. | `tf.linspace(0.0, 1.0, 5)`                                                                  |
| `tf.range`         | `start, limit=None, delta=1, dtype=None, name='range'`                     | Generates a sequence of values. <br> - `start`: Starting value. <br> - `limit`: (Optional) End value (exclusive). <br> - `delta`: Step size. <br> - `dtype`: (Optional) Data type of the values. | `tf.range(1, 10, 2)`                                                                        |
| `tf.random.uniform` | `shape, minval=0, maxval=None, dtype=tf.float32, seed=None, name=None`      | Creates a tensor with random values sampled from a uniform distribution. <br> - `shape`: Shape of the tensor. <br> - `minval`: Lower bound of the range. <br> - `maxval`: Upper bound (exclusive). <br> - `dtype`: (Optional) Data type of the tensor. <br> - `seed`: (Optional) Random seed. | `tf.random.uniform([2, 3], minval=0, maxval=10)`                                           |
| `tf.random.normal` | `shape, mean=0.0, stddev=1.0, dtype=tf.float32, seed=None, name=None`       | Creates a tensor with random values sampled from a normal (Gaussian) distribution. <br> - `shape`: Shape of the tensor. <br> - `mean`: Mean of the distribution. <br> - `stddev`: Standard deviation. <br> - `dtype`: (Optional) Data type of the tensor. <br> - `seed`: (Optional) Random seed. | `tf.random.normal([2, 3], mean=0, stddev=1)`                                               |
| `tf.random.truncated_normal` | `shape, mean=0.0, stddev=1.0, dtype=tf.float32, seed=None, name=None` | Creates a tensor with random values sampled from a truncated normal distribution (values beyond two standard deviations are discarded). <br> - `shape`: Shape of the tensor. <br> - `mean`: Mean of the distribution. <br> - `stddev`: Standard deviation. <br> - `dtype`: (Optional) Data type of the tensor. <br> - `seed`: (Optional) Random seed. | `tf.random.truncated_normal([2, 3], mean=0, stddev=1)`                                     |
| `tf.random.poisson` | `lam, shape, dtype=tf.float32, seed=None, name=None`                      | Generates random values sampled from a Poisson distribution. <br> - `lam`: Rate parameter (lambda). <br> - `shape`: Shape of the tensor. <br> - `dtype`: (Optional) Data type of the tensor. <br> - `seed`: (Optional) Random seed. | `tf.random.poisson(lam=5, shape=[2, 3])`                                                   |
| `tf.convert_to_tensor` | `value, dtype=None, dtype_hint=None, name=None`                         | Converts a Python object (e.g., list, NumPy array) to a TensorFlow tensor. <br> - `value`: Input object. <br> - `dtype`: (Optional) Data type of the output tensor. <br> - `dtype_hint`: (Optional) A preferred data type for type inference. | `tf.convert_to_tensor([1, 2, 3], dtype=tf.float32)`                                        |

---

### **2. Tensor Operations**

#### **Arithmetic Operations**

| Operation                | Parameters                                      | Description                                                                                              | Example                                                                                 |
|--------------------------|------------------------------------------------|----------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| `tf.add`                 | `x, y, name=None`                              | Element-wise addition of tensors `x` and `y`. <br> Broadcasts shapes if necessary.                       | `tf.add([1, 2], [3, 4])` → `[4, 6]`                                                   |
| `tf.subtract`            | `x, y, name=None`                              | Element-wise subtraction of `y` from `x`.                                                                | `tf.subtract([5, 3], [1, 2])` → `[4, 1]`                                              |
| `tf.multiply`            | `x, y, name=None`                              | Element-wise multiplication of tensors.                                                                  | `tf.multiply([2, 3], [4, 5])` → `[8, 15]`                                             |
| `tf.divide`              | `x, y, name=None`                              | Element-wise division of tensors.                                                                        | `tf.divide([10, 20], [2, 4])` → `[5, 5]`                                              |
| `tf.pow`                 | `x, y, name=None`                              | Computes element-wise power `x^y`.                                                                       | `tf.pow([2, 3], 2)` → `[4, 9]`                                                        |
| `tf.mod`                 | `x, y, name=None`                              | Computes element-wise modulus of `x` divided by `y`.                                                     | `tf.mod([10, 20], [3, 6])` → `[1, 2]`                                                 |

---

#### **Reduction Operations**

| Operation                | Parameters                                      | Description                                                                                              | Example                                                                                 |
|--------------------------|------------------------------------------------|----------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| `tf.reduce_sum`          | `input_tensor, axis=None, keepdims=False, name=None` | Computes the sum of elements across specified axes. <br> - `axis`: Axis/axes along which to reduce. <br> - `keepdims`: If `True`, retains reduced dimensions with size 1. | `tf.reduce_sum([[1, 2], [3, 4]], axis=0)` → `[4, 6]`                                   |
| `tf.reduce_mean`         | `input_tensor, axis=None, keepdims=False, name=None` | Computes the mean of elements across specified axes.                                                    | `tf.reduce_mean([[1, 2], [3, 4]], axis=1)` → `[1.5, 3.5]`                              |
| `tf.reduce_max`          | `input_tensor, axis=None, keepdims=False, name=None` | Finds the maximum element across specified axes.                                                        | `tf.reduce_max([[1, 2], [3, 4]])` → `4`                                               |
| `tf.reduce_min`          | `input_tensor, axis=None, keepdims=False, name=None` | Finds the minimum element across specified axes.                                                        | `tf.reduce_min([[1, 2], [3, 4]])` → `1`                                               |
| `tf.reduce_prod`         | `input_tensor, axis=None, keepdims=False, name=None` | Computes the product of elements across specified axes.                                                 | `tf.reduce_prod([1, 2, 3, 4])` → `24`                                                 |

---

#### **Matrix Operations**

| Operation                | Parameters                                      | Description                                                                                              | Example                                                                                 |
|--------------------------|------------------------------------------------|----------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| `tf.matmul`              | `a, b, transpose_a=False, transpose_b=False, name=None` | Performs matrix multiplication. <br> - `transpose_a`: Transposes `a` before multiplication if `True`. <br> - `transpose_b`: Transposes `b` before multiplication if `True`. | `tf.matmul([[1, 2]], [[3], [4]])` → `[[11]]`                                           |
| `tf.transpose`           | `a, perm=None, conjugate=False, name='transpose'` | Transposes the dimensions of a tensor. <br> - `perm`: (Optional) Permutation of dimensions.              | `tf.transpose([[1, 2], [3, 4]])` → `[[1, 3], [2, 4]]`                                  |
| `tf.linalg.inv`          | `input, adjoint=False, name=None`               | Computes the inverse of a square matrix.                                                                | `tf.linalg.inv([[4, 7], [2, 6]])` → `[[0.6, -0.7], [-0.2, 0.4]]`                       |
| `tf.linalg.det`          | `input, name=None`                              | Computes the determinant of a square matrix.                                                            | `tf.linalg.det([[4, 7], [2, 6]])` → `10.0`                                             |

---

#### **Comparison Operations**

| Operation                | Parameters                                      | Description                                                                                              | Example                                                                                 |
|--------------------------|------------------------------------------------|----------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| `tf.equal`               | `x, y, name=None`                              | Element-wise equality check. Returns a tensor of Boolean values.                                        | `tf.equal([1, 2], [1, 3])` → `[True, False]`                                           |
| `tf.not_equal`           | `x, y, name=None`                              | Element-wise inequality check.                                                                          | `tf.not_equal([1, 2], [1, 3])` → `[False, True]`                                       |
| `tf.greater`             | `x, y, name=None`                              | Element-wise greater-than check.                                                                        | `tf.greater([1, 2], [1, 3])` → `[False, False]`                                        |
| `tf.less`                | `x, y, name=None`                              | Element-wise less-than check.                                                                           | `tf.less([1, 2], [3, 2])` → `[True, False]`                                            |
| `tf.greater_equal`       | `x, y, name=None`                              | Element-wise greater-than-or-equal check.                                                               | `tf.greater_equal([1, 2], [1, 2])` → `[True, True]`                                    |
| `tf.less_equal`          | `x, y, name=None`                              | Element-wise less-than-or-equal check.                                                                  | `tf.less_equal([1, 2], [2, 1])` → `[True, False]`                                      |

---

#### **Logical Operations**

| Operation                | Parameters                                      | Description                                                                                              | Example                                                                                 |
|--------------------------|------------------------------------------------|----------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| `tf.logical_and`         | `x, y, name=None`                              | Element-wise logical AND.                                                                                | `tf.logical_and([True, False], [False, True])` → `[False, False]`                      |
| `tf.logical_or`          | `x, y, name=None`                              | Element-wise logical OR.                                                                                 | `tf.logical_or([True, False], [False, True])` → `[True, True]`                         |
| `tf.logical_not`         | `x, name=None`                                 | Element-wise logical NOT.                                                                                | `tf.logical_not([True, False])` → `[False, True]`                                      |

---

#### **Other Tensor Operations**

| Operation                | Parameters                                      | Description                                                                                              | Example                                                                                 |
|--------------------------|------------------------------------------------|----------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| `tf.reshape`             | `tensor, shape, name=None`                     | Reshapes a tensor to the specified shape.                                                                | `tf.reshape([1, 2, 3, 4], [2, 2])` → `[[1, 2], [3, 4]]`                                |
| `tf.expand_dims`         | `input, axis, name=None`                       | Adds a new dimension to a tensor at the specified axis.                                                  | `tf.expand_dims([1, 2, 3], axis=0)` → `[[1, 2, 3]]`                                    |
| `tf.squeeze`             | `input, axis=None, name=None`                  | Removes dimensions of size 1 from the shape of a tensor.                                                 | `tf.squeeze([[1], [2], [3]])` → `[1, 2, 3]`                                            |

---

### **3. Tensor Attributes**

| **Attribute**      | **Description**                                                                                               | **Example Code**                                                                       | **Example Output**                 |
|---------------------|---------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|-------------------------------------|
| `tf.Tensor.shape`   | Returns the **shape** of the tensor as a `tf.TensorShape` object. Shape represents the dimensions of the tensor. | `tensor = tf.constant([[1, 2], [3, 4]])` <br> `tensor.shape`                           | `(2, 2)`                           |
| `tf.Tensor.dtype`   | Returns the **data type** of the elements stored in the tensor, e.g., `tf.int32`, `tf.float32`, etc.           | `tensor = tf.constant([1.0, 2.0, 3.0])` <br> `tensor.dtype`                            | `tf.float32`                       |
| `tf.Tensor.name`    | Returns the **name** of the tensor in a graph (useful in graph-based execution). Default is an empty string.   | `tensor = tf.constant(10, name="my_tensor")` <br> `tensor.name`                        | `'my_tensor:0'`                    |
| `tf.Tensor.rank`    | Returns the **rank** (number of dimensions) of the tensor.                                                    | `tensor = tf.constant([1, 2, 3])` <br> `tf.rank(tensor)`                               | `1`                                 |
| `tf.Tensor.device`  | Indicates the **device** (CPU, GPU, etc.) where the tensor is stored.                                         | `tensor = tf.constant(5)` <br> `tensor.device`                                         | `'CPU:0'` or `'GPU:0'`             |
| `tf.Tensor.numpy()` | Converts the tensor to a NumPy array. Useful for interoperability with NumPy-based operations.                | `tensor = tf.constant([1, 2, 3])` <br> `tensor.numpy()`                                | `[1, 2, 3]`                        |
| `tf.Tensor.op`      | Provides information about the **operation** that produced the tensor (graph mode only).                      | `tensor = tf.constant(10, name="my_tensor")` <br> `tensor.op`                          | `<tf.Operation 'my_tensor'...>`    |
| `tf.Tensor.ref`     | Gives a **reference** to the tensor for dynamic shapes (useful in advanced TensorFlow workflows).             | `tensor = tf.Variable([1, 2, 3])` <br> `tensor.ref()`                                  | TensorFlow reference object output |

---

#### **Examples Explained**

1. **Shape**:
   - **What it does**: Provides the dimensionality of the tensor.
   - **Use case**: Useful for debugging or when reshaping tensors.
   ```python
   tensor = tf.constant([[1, 2], [3, 4], [5, 6]])
   print(tensor.shape)  # Output: (3, 2)
   ```

2. **Data Type**:
   - **What it does**: Helps ensure compatibility in operations involving mixed types.
   - **Use case**: Ensuring precision by checking `dtype`.
   ```python
   tensor = tf.constant([1.0, 2.0, 3.0])
   print(tensor.dtype)  # Output: tf.float32
   ```

3. **Name**:
   - **What it does**: Helps trace specific tensors in graph-based execution.
   - **Use case**: Useful when debugging complex models.
   ```python
   tensor = tf.constant(5, name="example_tensor")
   print(tensor.name)  # Output: 'example_tensor:0'
   ```

4. **Device**:
   - **What it does**: Indicates where the tensor is stored (CPU/GPU).
   - **Use case**: Ensuring tensor placement on GPUs for faster computation.
   ```python
   tensor = tf.constant(10)
   print(tensor.device)  # Output: '/job:localhost/replica:0/task:0/device:CPU:0'
   ```

5. **NumPy Conversion**:
   - **What it does**: Converts tensors to NumPy for further processing.
   - **Use case**: Bridging TensorFlow and NumPy workflows.
   ```python
   tensor = tf.constant([1, 2, 3])
   print(tensor.numpy())  # Output: [1 2 3]
   ```

6. **Rank**:
   - **What it does**: Returns the number of dimensions of the tensor.
   - **Use case**: Understanding tensor complexity.
   ```python
   tensor = tf.constant([[[1, 2], [3, 4]]])
   print(tf.rank(tensor))  # Output: 3
   ```

---

### **4. Reshaping and Slicing**

---

#### **Reshaping Tensors**

| **Operation**                   | **Description**                                                                                   | **Parameters**                                                                                 | **Example Code**                                                                    | **Output**                            |
|----------------------------------|---------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|---------------------------------------|
| `tf.reshape(tensor, shape)`      | Changes the shape of a tensor without altering its data.                                          | - **tensor**: Input tensor <br> - **shape**: Desired shape; use `-1` for auto-dimension        | `tensor = tf.constant([[1, 2], [3, 4]])` <br> `tf.reshape(tensor, [4])`             | `[1, 2, 3, 4]`                        |
| `tf.expand_dims(tensor, axis)`   | Adds a new dimension to the tensor at the specified axis.                                         | - **axis**: Position of new dimension                                                         | `tensor = tf.constant([1, 2, 3])` <br> `tf.expand_dims(tensor, axis=0)`             | `[[1, 2, 3]]`                         |
| `tf.squeeze(tensor, axis=None)`  | Removes dimensions of size 1 from the shape of the tensor.                                       | - **axis**: Axis to squeeze (optional)                                                        | `tensor = tf.constant([[[1], [2], [3]]])` <br> `tf.squeeze(tensor)`                 | `[1, 2, 3]`                           |
| `tf.transpose(tensor, perm)`     | Permutes the dimensions of the tensor according to the specified order.                          | - **perm**: A list of dimension indices                                                       | `tensor = tf.constant([[1, 2], [3, 4]])` <br> `tf.transpose(tensor, perm=[1, 0])`   | `[[1, 3], [2, 4]]`                    |

---

##### **Examples for Reshaping**

1. **Basic Reshape**:
   ```python
   tensor = tf.constant([[1, 2], [3, 4]])
   reshaped = tf.reshape(tensor, [4])
   print(reshaped)  # Output: [1, 2, 3, 4]
   ```

2. **Expand Dimensions**:
   ```python
   tensor = tf.constant([1, 2, 3])
   expanded = tf.expand_dims(tensor, axis=1)
   print(expanded)  # Output: [[1], [2], [3]]
   ```

3. **Squeeze Dimensions**:
   ```python
   tensor = tf.constant([[[1], [2], [3]]])
   squeezed = tf.squeeze(tensor)
   print(squeezed)  # Output: [1, 2, 3]
   ```

---

#### **Slicing Tensors**

| **Operation**                   | **Description**                                                                                   | **Parameters**                                                                                 | **Example Code**                                                                    | **Output**                            |
|----------------------------------|---------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|---------------------------------------|
| `tensor[start:stop:step]`        | Extracts a slice along a given axis (similar to Python slicing).                                  | - **start**: Start index <br> - **stop**: End index (exclusive) <br> - **step**: Step size     | `tensor = tf.constant([1, 2, 3, 4, 5])` <br> `tensor[1:4]`                         | `[2, 3, 4]`                           |
| `tf.slice(tensor, begin, size)`  | Extracts a sub-tensor by specifying start indices and size for each dimension.                   | - **begin**: Start indices <br> - **size**: Size for each dimension                           | `tensor = tf.constant([[1, 2], [3, 4], [5, 6]])` <br> `tf.slice(tensor, [0, 0], [2, 2])` | `[[1, 2], [3, 4]]`                   |
| `tensor[..., indices]`           | Advanced slicing to extract specific elements using ellipsis (`...`) for unspecified dimensions. | - **...**: Placeholder for unspecified dimensions                                             | `tensor = tf.constant([[[1, 2], [3, 4]], [[5, 6], [7, 8]]])` <br> `tensor[..., 1]`   | `[[2, 4], [6, 8]]`                   |

---

##### **Examples for Slicing**

1. **Simple Slicing**:
   ```python
   tensor = tf.constant([1, 2, 3, 4, 5])
   sliced = tensor[1:4]
   print(sliced)  # Output: [2, 3, 4]
   ```

2. **Using `tf.slice`**:
   ```python
   tensor = tf.constant([[1, 2], [3, 4], [5, 6]])
   sliced = tf.slice(tensor, [0, 0], [2, 2])
   print(sliced)  # Output: [[1, 2], [3, 4]]
   ```

3. **Ellipsis Slicing**:
   ```python
   tensor = tf.constant([[[1, 2], [3, 4]], [[5, 6], [7, 8]]])
   result = tensor[..., 1]
   print(result)  # Output: [[2, 4], [6, 8]]
   ```

---

##### **Comparison of Slicing Methods**

| **Method**       | **Flexibility**            | **Ease of Use**         | **Use Case**                  |
|-------------------|----------------------------|--------------------------|--------------------------------|
| Python-like `[]`  | Best for simple slicing    | Intuitive and concise    | Small slices or single-axis   |
| `tf.slice`        | Precise for multi-axis     | Requires detailed input  | Complex multi-axis operations |
| Ellipsis `...`    | Flexible with broadcasting | Easy for higher-rank ops | Slicing with skipped axes     |

---

#### **Indexing and Masking**

| **Operation**                   | **Description**                                                                                   | **Parameters**                                                                                 | **Example Code**                                                                    | **Output**                            |
|----------------------------------|---------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|---------------------------------------|
| `tensor[index]`                  | Extracts elements using standard indexing (like NumPy).                                           | - **index**: Index of the element to be retrieved                                             | `tensor = tf.constant([1, 2, 3, 4])` <br> `tensor[2]`                              | `3`                                   |
| `tf.gather(tensor, indices)`     | Gathers slices of a tensor according to the specified indices.                                    | - **tensor**: Input tensor <br> - **indices**: Indices for selection                         | `tensor = tf.constant([1, 2, 3, 4])` <br> `tf.gather(tensor, [0, 3])`              | `[1, 4]`                              |
| `tf.boolean_mask(tensor, mask)`  | Extracts elements of a tensor using a mask (Boolean array).                                       | - **mask**: Boolean mask of the same shape as the tensor.                                     | `tensor = tf.constant([1, 2, 3, 4])` <br> `mask = [True, False, True, False]` <br> `tf.boolean_mask(tensor, mask)` | `[1, 3]`                              |

---

### **5. Broadcasting**

#### **Broadcasting in TensorFlow**

Broadcasting is a technique that allows TensorFlow to perform operations on tensors of different shapes by automatically expanding their dimensions to make them compatible.

---

#### **Broadcasting Rules**
1. **Rank Adjustment**: If two tensors have different ranks, the smaller-rank tensor is padded with dimensions of size `1` on the left.
2. **Dimension Compatibility**: Two dimensions are compatible if:
   - They are equal, or
   - One of them is `1`.
3. **Resulting Shape**: After broadcasting, each dimension of the tensors must match, or one must be `1`.

---

#### **Examples of Broadcasting**

| **Operation**                | **Description**                        | **Tensor A**                      | **Tensor B**                  | **Result**                       |
|-------------------------------|----------------------------------------|------------------------------------|--------------------------------|-----------------------------------|
| Add scalar to tensor          | Scalar is broadcast to match tensor    | `[[1, 2], [3, 4]]` (shape: `[2,2]`) | `5` (shape: `[]`)              | `[[6, 7], [8, 9]]`               |
| Add row vector to matrix      | Row vector is broadcast to match rows | `[[1, 2], [3, 4]]` (shape: `[2,2]`) | `[5, 6]` (shape: `[2]`)        | `[[6, 8], [8, 10]]`              |
| Add column vector to matrix   | Column vector is broadcast to match cols | `[[1, 2], [3, 4]]` (shape: `[2,2]`) | `[[10], [20]]` (shape: `[2,1]`) | `[[11, 12], [23, 24]]`           |

---

#### **Common TensorFlow Broadcasting Operations**

| **Operation**         | **Tensor A**                           | **Tensor B**                           | **Result**                                 |
|------------------------|----------------------------------------|----------------------------------------|-------------------------------------------|
| `tf.add(A, B)`         | `[[1, 2], [3, 4]]`                    | `[10, 20]`                             | `[[11, 22], [13, 24]]`                    |
| `tf.multiply(A, B)`    | `[[1, 2], [3, 4]]`                    | `[10]`                                 | `[[10, 20], [30, 40]]`                    |
| `tf.subtract(A, B)`    | `[[5, 10], [15, 20]]`                 | `[1, 2]`                               | `[[4, 8], [14, 18]]`                      |
| `tf.divide(A, B)`      | `[[10, 20], [30, 40]]`                | `10`                                   | `[[1, 2], [3, 4]]`                        |
| `tf.pow(A, B)`         | `[[2, 3], [4, 5]]`                    | `[2, 3]`                               | `[[4, 27], [16, 125]]`                    |

---

#### **Broadcasting Scenarios**

| **Scenario**          | **Input Shapes**     | **Broadcasted Shapes**       | **Explanation**                                                   |
|------------------------|----------------------|-------------------------------|-------------------------------------------------------------------|
| Scalar with Tensor     | `[3, 3]` vs `[]`    | `[3, 3]`                      | Scalar expands to match tensor dimensions.                       |
| Vector with Matrix     | `[3, 3]` vs `[3]`   | `[3, 3]`                      | Row vector broadcasts across rows of the matrix.                 |
| Higher-Rank Tensors    | `[2, 3, 4]` vs `[3, 4]` | `[2, 3, 4]`                 | Lower-rank tensor is padded with dimensions of size 1.            |
| Mismatched Dimensions  | `[3, 1]` vs `[1, 4]` | `[3, 4]`                     | Singleton dimensions expand to match the other tensor’s size.     |

---

#### **Examples in TensorFlow**

1. **Scalar with Tensor**:
   ```python
   A = tf.constant([[1, 2], [3, 4]])
   B = tf.constant(5)  # Scalar
   result = tf.add(A, B)
   print(result)  # Output: [[6, 7], [8, 9]]
   ```

2. **Vector with Matrix**:
   ```python
   A = tf.constant([[1, 2], [3, 4]])
   B = tf.constant([10, 20])  # Row vector
   result = tf.add(A, B)
   print(result)  # Output: [[11, 22], [13, 24]]
   ```

3. **Higher-Rank Tensors**:
   ```python
   A = tf.constant([[[1, 2, 3]], [[4, 5, 6]]])  # Shape: [2, 1, 3]
   B = tf.constant([10, 20, 30])  # Shape: [3]
   result = tf.add(A, B)
   print(result)  # Output: [[[11, 22, 33]], [[14, 25, 36]]]
   ```

---

#### **Broadcasting Exceptions**
Broadcasting fails if the dimensions are incompatible:
1. **Mismatch in non-singleton dimensions**: Dimensions that aren't `1` or equal result in an error.
2. **Example**:
   ```python
   A = tf.constant([[1, 2], [3, 4]])  # Shape: [2, 2]
   B = tf.constant([10, 20, 30])  # Shape: [3]
   # Throws an error because shapes [2, 2] and [3] are incompatible.
   ```

---

### **6. Tensor Types in TensorFlow**

In TensorFlow, tensors can have various types based on their data type, rank, or structure. The data type of a tensor determines the kind of data it holds. TensorFlow supports a wide range of tensor data types, broadly categorized as numeric, string, boolean, and complex types.

---

#### **Tensor Data Types**

| **Data Type**          | **DType**                | **Description**                                                                                  | **Example Usage**                |
|-------------------------|--------------------------|--------------------------------------------------------------------------------------------------|-----------------------------------|
| Integer Types           | `tf.int8`, `tf.int16`, `tf.int32`, `tf.int64` | Signed integers of varying sizes (`8`, `16`, `32`, `64` bits).                                  | Tensor for counting or indexing. |
| Unsigned Integer Types  | `tf.uint8`, `tf.uint16`  | Unsigned integers for non-negative values.                                                      | Image processing (e.g., RGB).    |
| Floating-Point Types    | `tf.float16`, `tf.float32`, `tf.float64` | Floating-point numbers of varying precision.                                                    | General numeric computations.    |
| Complex Types           | `tf.complex64`, `tf.complex128` | Complex numbers with 32-bit or 64-bit real and imaginary parts.                                  | Fourier transforms.              |
| Boolean Type            | `tf.bool`               | Boolean values (`True` or `False`).                                                             | Logical operations.              |
| String Type             | `tf.string`             | Variable-length byte strings.                                                                   | Text data or embeddings.         |
| Quantized Types         | `tf.qint8`, `tf.qint32`, `tf.quint8` | Quantized integers for reducing model size and memory usage.                                    | Quantized neural networks.       |
| BFloat Type             | `tf.bfloat16`           | A 16-bit floating-point format with less precision but a wider dynamic range than `float16`.    | TPU training acceleration.       |
| Resource Type           | `tf.resource`           | Handles for mutable resources like variables.                                                   | Variables and states.            |
| Variant Type            | `tf.variant`            | Arbitrary custom types or composite data structures.                                            | Tensor arrays or sparse tensors. |
| Half Precision Type     | `tf.float16`            | Half-precision (16-bit) floating-point type.                                                    | Low-memory GPU operations.       |

---

#### **Attributes of Tensor Data Types**

| **Attribute**     | **Description**                                 | **Example**                                |
|--------------------|------------------------------------------------|-------------------------------------------|
| `dtype`           | Data type of elements in the tensor.            | `tf.float32`                              |
| `numpy`           | Numpy representation of tensor values.          | `tensor.numpy()`                          |
| `shape`           | Shape of the tensor, showing dimensions.        | `(3, 2)`                                  |
| `ndim`            | Rank (number of dimensions) of the tensor.      | `2` (for a matrix)                        |
| `device`          | Device where the tensor is stored (CPU/GPU).    | `/job:localhost/replica:0/task:0/device:CPU:0` |

---

#### **Examples of Tensor Types**

1. **Integer Tensor**:
   ```python
   tensor = tf.constant([1, 2, 3], dtype=tf.int32)
   print(tensor)
   # Output: <tf.Tensor: shape=(3,), dtype=int32, numpy=array([1, 2, 3], dtype=int32)>
   ```

2. **Float Tensor**:
   ```python
   tensor = tf.constant([1.1, 2.2, 3.3], dtype=tf.float32)
   print(tensor)
   # Output: <tf.Tensor: shape=(3,), dtype=float32, numpy=array([1.1, 2.2, 3.3], dtype=float32)>
   ```

3. **Boolean Tensor**:
   ```python
   tensor = tf.constant([True, False, True], dtype=tf.bool)
   print(tensor)
   # Output: <tf.Tensor: shape=(3,), dtype=bool, numpy=array([ True, False,  True])>
   ```

4. **String Tensor**:
   ```python
   tensor = tf.constant(["TensorFlow", "is", "awesome"], dtype=tf.string)
   print(tensor)
   # Output: <tf.Tensor: shape=(3,), dtype=string, numpy=array([b'TensorFlow', b'is', b'awesome'], dtype=object)>
   ```

5. **Complex Tensor**:
   ```python
   tensor = tf.constant([1+2j, 3+4j], dtype=tf.complex64)
   print(tensor)
   # Output: <tf.Tensor: shape=(2,), dtype=complex64, numpy=array([1.+2.j, 3.+4.j], dtype=complex64)>
   ```

---

#### **Default Tensor Types in TensorFlow**

- Default data type for **numeric constants**: `tf.float32`.
- Default data type for **integer constants**: `tf.int32`.

---

#### **Casting Between Types**

| **Function**                  | **Description**                                   | **Example**                         |
|-------------------------------|--------------------------------------------------|-------------------------------------|
| `tf.cast(x, dtype)`           | Casts tensor `x` to a new data type `dtype`.     | `tf.cast([1.1, 2.2], tf.int32)`     |
| `tf.dtypes.as_dtype(type)`    | Converts Python types to TensorFlow data types.  | `tf.dtypes.as_dtype(int)`           |
| `tf.dtypes.cast(x, dtype)`    | Similar to `tf.cast` for casting tensors.        | `tf.dtypes.cast([True], tf.int32)`  |

---

#### **Notes for Tensor Types**
1. Use data types matching your hardware:
   - **`tf.float16` or `tf.bfloat16`** for GPUs/TPUs.
   - **`tf.float32`** for general computations.
2. Always cast explicitly to avoid unintended data loss or precision issues.

---

### **7. Common Tensor Functions**

---

#### **Tensor Utility Functions**

| **Function**            | **Description**                                                                                  | **Example**                                                |
|-------------------------|--------------------------------------------------------------------------------------------------|------------------------------------------------------------|
| `tf.is_tensor(x)`       | Checks if `x` is a TensorFlow tensor.                                                           | `tf.is_tensor(tf.constant([1, 2, 3]))  # True`             |
| `tf.convert_to_tensor(x)` | Converts a Python object or Numpy array to a TensorFlow tensor.                                | `tf.convert_to_tensor([1, 2, 3])`                          |
| `tf.identity(x)`        | Returns a tensor with the same value as `x`. Useful for cloning tensors.                        | `tf.identity(tf.constant([1, 2]))`                        |
| `tf.stop_gradient(x)`   | Stops the gradient computation for the tensor `x`.                                              | `tf.stop_gradient(tf.constant([1, 2]))`                   |
| `tf.rank(x)`            | Returns the rank (number of dimensions) of a tensor.                                            | `tf.rank(tf.constant([[1, 2], [3, 4]]))  # 2`             |
| `tf.size(x)`            | Returns the total number of elements in the tensor.                                             | `tf.size(tf.constant([[1, 2], [3, 4]]))  # 4`             |

---

#### **Shape Manipulation Functions**

| **Function**            | **Description**                                                                                  | **Example**                                                |
|-------------------------|--------------------------------------------------------------------------------------------------|------------------------------------------------------------|
| `tf.shape(x)`           | Returns the shape of the tensor as a 1-D tensor.                                                | `tf.shape(tf.constant([[1, 2], [3, 4]]))`                 |
| `tf.reshape(x, shape)`  | Changes the shape of the tensor to the specified `shape`.                                        | `tf.reshape(tf.constant([1, 2, 3, 4]), [2, 2])`           |
| `tf.expand_dims(x, axis)` | Adds a new dimension to the tensor at the specified `axis`.                                    | `tf.expand_dims(tf.constant([1, 2, 3]), axis=0)`          |
| `tf.squeeze(x, axis)`   | Removes dimensions of size 1 from the shape of a tensor.                                        | `tf.squeeze(tf.constant([[1], [2], [3]]), axis=1)`         |
| `tf.transpose(x, perm)` | Permutes the dimensions of a tensor according to `perm`.                                        | `tf.transpose(tf.constant([[1, 2], [3, 4]]))`             |

---

#### **Data Type Manipulation Functions**

| **Function**            | **Description**                                                                                  | **Example**                                                |
|-------------------------|--------------------------------------------------------------------------------------------------|------------------------------------------------------------|
| `tf.cast(x, dtype)`     | Casts a tensor to a specified data type.                                                        | `tf.cast(tf.constant([1, 2]), tf.float32)`                |
| `tf.dtypes.as_dtype(type)` | Converts a Python type or NumPy dtype to a TensorFlow `DType`.                               | `tf.dtypes.as_dtype(int)`                                  |
| `tf.dtypes.is_integer(dtype)` | Checks if the data type is an integer type.                                               | `tf.dtypes.is_integer(tf.int32)`                          |
| `tf.dtypes.is_floating(dtype)` | Checks if the data type is a floating-point type.                                        | `tf.dtypes.is_floating(tf.float64)`                       |

---

#### **Tensor Algebra and Linear Algebra Utilities**

| **Function**            | **Description**                                                                                  | **Example**                                                |
|-------------------------|--------------------------------------------------------------------------------------------------|------------------------------------------------------------|
| `tf.linalg.norm(x)`     | Computes the Euclidean norm (or other norms) of the tensor.                                      | `tf.linalg.norm(tf.constant([3, 4]))  # 5`                |
| `tf.linalg.inv(x)`      | Computes the inverse of a square matrix.                                                        | `tf.linalg.inv(tf.constant([[1, 2], [3, 4]]))`            |
| `tf.linalg.matmul(a, b)` | Performs matrix multiplication on two tensors.                                                 | `tf.linalg.matmul(tf.constant([[1, 2]]), tf.constant([[3], [4]]))` |
| `tf.linalg.det(x)`      | Computes the determinant of a square matrix.                                                    | `tf.linalg.det(tf.constant([[1, 2], [3, 4]]))`            |
| `tf.linalg.eigvals(x)`  | Computes the eigenvalues of a square matrix.                                                    | `tf.linalg.eigvals(tf.constant([[1, 2], [3, 4]]))`        |

---

#### **Tensor Aggregation Functions**

| **Function**            | **Description**                                                                                  | **Example**                                                |
|-------------------------|--------------------------------------------------------------------------------------------------|------------------------------------------------------------|
| `tf.reduce_sum(x, axis)` | Computes the sum of elements along a specified axis.                                           | `tf.reduce_sum(tf.constant([[1, 2], [3, 4]]), axis=0)`     |
| `tf.reduce_mean(x, axis)` | Computes the mean of elements along a specified axis.                                         | `tf.reduce_mean(tf.constant([[1, 2], [3, 4]]), axis=1)`    |
| `tf.reduce_max(x, axis)` | Computes the maximum of elements along a specified axis.                                       | `tf.reduce_max(tf.constant([[1, 2], [3, 4]]), axis=1)`     |
| `tf.reduce_min(x, axis)` | Computes the minimum of elements along a specified axis.                                       | `tf.reduce_min(tf.constant([[1, 2], [3, 4]]), axis=0)`     |
| `tf.reduce_prod(x, axis)` | Computes the product of elements along a specified axis.                                      | `tf.reduce_prod(tf.constant([[1, 2], [3, 4]]), axis=0)`    |
| `tf.reduce_any(x, axis)` | Computes logical OR across elements along a specified axis.                                    | `tf.reduce_any(tf.constant([[True, False], [False, False]]))` |
| `tf.reduce_all(x, axis)` | Computes logical AND across elements along a specified axis.                                   | `tf.reduce_all(tf.constant([[True, False], [True, True]]))` |

---

#### **Tensor Inspection and Debugging Functions**

| **Function**              | **Description**                                                                                 | **Example**                                                |
|---------------------------|-------------------------------------------------------------------------------------------------|------------------------------------------------------------|
| `tf.debugging.assert_rank(x, rank)` | Asserts that a tensor has the specified rank.                                        | `tf.debugging.assert_rank(tf.constant([1, 2, 3]), rank=1)` |
| `tf.debugging.assert_non_negative(x)` | Asserts that all elements in a tensor are non-negative.                            | `tf.debugging.assert_non_negative(tf.constant([1, 2]))`    |
| `tf.debugging.check_numerics(x, message)` | Checks if the tensor contains `NaN` or `Inf`.                                   | `tf.debugging.check_numerics(tf.constant([1, float('nan')]), "Error")` |

---

#### **Other Utility Functions**

| **Function**              | **Description**                                                                                 | **Example**                                                |
|---------------------------|-------------------------------------------------------------------------------------------------|------------------------------------------------------------|
| `tf.boolean_mask(tensor, mask)` | Applies a boolean mask to a tensor to extract selected elements.                          | `tf.boolean_mask(tf.constant([1, 2, 3]), [True, False, True])` |
| `tf.where(condition, x, y)` | Returns elements from `x` or `y`, depending on `condition`.                                   | `tf.where(tf.constant([True, False]), x=1, y=0)`           |
| `tf.gather(params, indices, axis)` | Gathers slices from `params` along the specified axis using `indices`.                  | `tf.gather([1, 2, 3], [0, 2])`                            |               |
