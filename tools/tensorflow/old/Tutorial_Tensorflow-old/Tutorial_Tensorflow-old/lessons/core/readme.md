## Core TensorFlow Concepts

#### **1. Tensors**
A **tensor** is the central unit of data in TensorFlow. It is a generalization of vectors and matrices to potentially higher dimensions.

| **Term**        | **Description**                                                                                     | **Example**            |
|------------------|-----------------------------------------------------------------------------------------------------|------------------------|
| **Rank**         | Number of dimensions (0D = scalar, 1D = vector, 2D = matrix, etc.)                                  | Rank-2: `[[1, 2], [3, 4]]` |
| **Shape**        | Size of each dimension of the tensor                                                               | `[2, 2]` for the above example |
| **Data Types**   | Type of data stored in the tensor (e.g., `float32`, `int32`, `bool`, etc.)                          | `tf.constant([1, 2], dtype=tf.int32)` |
| **Broadcasting** | Ability to perform operations on tensors of different shapes                                        | Adding scalar to a matrix |

#### **Tensor Ranks and Shapes**

| **Rank** | **Name**       | **Example**                         |
|----------|----------------|-------------------------------------|
| 0        | Scalar         | `5`                                |
| 1        | Vector         | `[1, 2, 3]`                        |
| 2        | Matrix         | `[[1, 2], [3, 4]]`                 |
| 3        | 3-Tensor       | `[[[1, 2], [3, 4]], [[5, 6], [7, 8]]]` |
| N        | N-Tensor       | Higher-dimensional generalizations |

#### **Tensor Operations**

| **Operation**          | **Description**                          | **Example**                                      |
|-------------------------|------------------------------------------|------------------------------------------------|
| Element-wise operations | Operations applied to each tensor element| `tf.add(x, y)`                                 |
| Matrix operations       | Includes dot products, matrix multiplication | `tf.matmul(A, B)`                              |
| Reshaping               | Changing the shape without altering data | `tf.reshape(tensor, [new_shape])`             |
| Broadcasting            | Automatically expands smaller dimensions | `tf.add([1, 2, 3], [[4], [5], [6]])`          |

---

#### **2. Operations (Ops)**
TensorFlow operations perform computations on tensors, from basic math to complex matrix operations.

| **Category**               | **Common Operations**                                                                 | **Usage**                                          |
|----------------------------|---------------------------------------------------------------------------------------|--------------------------------------------------|
| **Math Operations**        | `tf.add`, `tf.subtract`, `tf.multiply`, `tf.divide`, `tf.pow`, `tf.sqrt`             | Element-wise math operations                     |
| **Reduction Operations**   | `tf.reduce_sum`, `tf.reduce_mean`, `tf.reduce_max`, `tf.reduce_min`                  | Aggregating tensors                              |
| **Array Manipulations**    | `tf.concat`, `tf.slice`, `tf.tile`, `tf.gather`, `tf.scatter_nd`                      | Changing shape or elements of tensors            |
| **Logical Operations**     | `tf.equal`, `tf.greater`, `tf.less`, `tf.logical_and`, `tf.logical_or`               | Logical comparisons and decisions                |
| **Custom Operations**      | Define custom operations using `tf.function`                                         | Optimizing repetitive logic                      |

---

#### **3. Graphs and Eager Execution**
TensorFlow allows two execution modes: **Eager Execution** (default) and **Graph Execution**.

| **Execution Mode**    | **Description**                                                                                     | **Example**                               |
|-----------------------|-----------------------------------------------------------------------------------------------------|------------------------------------------|
| **Eager Execution**   | Operations are executed immediately in a Python-like manner                                         | `tf.add(1, 2)` results in `3` instantly  |
| **Graph Execution**   | Builds a computational graph for optimization and later execution (`tf.function` for defining graphs)| Faster execution for large computations  |

---

#### **Eager vs. Graph Mode Comparison**

| **Feature**          | **Eager Execution**                            | **Graph Execution**                    |
|-----------------------|------------------------------------------------|----------------------------------------|
| **Speed**            | Slower, as operations execute immediately      | Optimized for speed with precompiled graphs |
| **Debugging**        | Easier, Python-like                            | Harder, as graphs must be debugged     |
| **Flexibility**      | High                                           | Limited to predefined graph structures |

---
