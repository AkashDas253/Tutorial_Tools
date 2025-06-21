## Sessions

In TensorFlow, **sessions** are an important concept in TensorFlow 1.x, where computation graphs are defined and executed within a session. In TensorFlow 2.x, eager execution is enabled by default, and you don't have to explicitly create a session to run operations. However, TensorFlow still supports sessions through `tf.compat.v1.Session`, which is useful for maintaining compatibility with older code.

Let's explore **sessions** in detail.

### **1. What is a Session?**
A session in TensorFlow is an environment where operations (like addition, multiplication, etc.) are executed. It encapsulates the state of the TensorFlow runtime and the operations performed.

#### Key Functions in Session (TensorFlow 1.x)
In TensorFlow 1.x, the computation graph is built first and then executed inside a session. Here are the key session functions:

| Function                   | Parameters                                   | Description                                                                                                         | Example                                                                 |
|----------------------------|----------------------------------------------|---------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| **`tf.Session()`**          | None                                         | Creates a new TensorFlow session, which is used to execute operations in the graph.                                  | `sess = tf.Session()`                                                  |
| **`session.run()`**         | `fetches, feed_dict=None, **kwargs`           | Executes one or more operations in the graph and returns the output. <br> - `fetches`: Operation or tensor to run.  | `sess.run(fetches=[a, b], feed_dict={x: x_value, y: y_value})`         |
| **`session.close()`**       | None                                         | Closes the session, releasing resources.                                                                            | `sess.close()`                                                         |
| **`session.graph`**         | None                                         | Returns the graph that the session is running on.                                                                   | `graph = sess.graph`                                                   |

### **2. Eager Execution in TensorFlow 2.x**
In TensorFlow 2.x, eager execution is the default mode, which means operations are evaluated immediately as they are called. There’s no need for a session to execute operations. TensorFlow 2.x uses Python’s native execution model, where each operation is evaluated as it’s called.

Example in TensorFlow 2.x (eager execution is enabled by default):
```python
import tensorflow as tf

# TensorFlow 2.x code does not require sessions
a = tf.constant(5)
b = tf.constant(3)
c = a + b
print(c.numpy())  # Direct evaluation without a session
```

### **3. Using `tf.compat.v1.Session` in TensorFlow 2.x**
If you want to use a session (for compatibility with older code or TensorFlow 1.x), you can disable eager execution and use `tf.compat.v1.Session`.

| Function                    | Parameters                                    | Description                                                                                                  | Example                                                         |
|-----------------------------|-----------------------------------------------|--------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------|
| **`tf.compat.v1.Session()`** | None                                          | Creates a TensorFlow session for compatibility with TensorFlow 1.x.                                          | `sess = tf.compat.v1.Session()`                                 |
| **`sess.run()`**             | `fetches, feed_dict=None, **kwargs`            | Runs the operations inside the session.                                                                        | `sess.run(fetches=[a, b], feed_dict={x: x_value, y: y_value})`  |
| **`sess.close()`**           | None                                          | Closes the session and frees resources.                                                                       | `sess.close()`                                                   |

#### Example of Using a Session in TensorFlow 2.x with Compatibility Mode:
```python
import tensorflow as tf

# Disable eager execution to use sessions
tf.compat.v1.disable_eager_execution()

# Create some operations in the graph
a = tf.compat.v1.constant(5)
b = tf.compat.v1.constant(3)
c = a + b

# Create a session and run the operations
with tf.compat.v1.Session() as sess:
    result = sess.run(c)
    print(result)  # Output: 8
```

### **4. Placeholder Variables in Sessions (TensorFlow 1.x)**
In TensorFlow 1.x, placeholders were used to provide data to the graph during session execution. They allow TensorFlow to run operations with different inputs each time.

| Function                   | Parameters                                   | Description                                                                                                         | Example                                                                 |
|----------------------------|----------------------------------------------|---------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| **`tf.placeholder()`**      | `dtype, shape=None, name=None`               | Used to define a placeholder tensor for input data. <br> - `dtype`: Data type of the placeholder.                 | `x = tf.placeholder(tf.float32, shape=[None, 3])`                     |
| **`feed_dict` in session.run()`** | `feed_dict={}`                              | Used to feed data to placeholders during session execution.                                                        | `sess.run(a, feed_dict={x: np.array([1, 2, 3])})`                     |

#### Example with Placeholder:
```python
import tensorflow as tf
import numpy as np

# Define placeholders
x = tf.compat.v1.placeholder(tf.float32, shape=[None, 3])
y = tf.compat.v1.placeholder(tf.float32, shape=[None, 3])

# Define an operation
z = x + y

# Start a session
with tf.compat.v1.Session() as sess:
    # Run the operation with feed_dict to feed values to placeholders
    result = sess.run(z, feed_dict={x: np.array([[1, 2, 3]]), y: np.array([[4, 5, 6]])})
    print(result)  # Output: [[5. 7. 9.]]
```

### **5. Switching Back to Eager Execution**
If you are using `tf.compat.v1.Session()` for legacy code and want to return to eager execution mode, you can enable it manually.

```python
tf.compat.v1.enable_eager_execution()
```

### **6. TensorFlow 2.x vs TensorFlow 1.x Sessions**
- **TensorFlow 1.x** uses `tf.Session()` and builds graphs explicitly before running them.
- **TensorFlow 2.x** uses eager execution by default, which means no session is required to evaluate operations.

---

### **Summary:**
- **Sessions** in TensorFlow are used for evaluating a computation graph.
- In **TensorFlow 1.x**, sessions were explicitly used to run operations within a graph.
- In **TensorFlow 2.x**, eager execution is enabled by default, meaning operations are evaluated immediately and don't require sessions.
- **`tf.compat.v1.Session()`** is available for compatibility with TensorFlow 1.x code.

By understanding sessions, you can choose between eager execution for simplicity or use the session-based approach for legacy code and optimization needs.