# Execution Modes

---

## Definition

TensorFlow supports two primary execution modes that determine **how operations are executed**:

* **Eager Execution**
* **Graph Execution (a.k.a. Lazy/Deferred Execution)**

Each mode affects performance, debuggability, and deployment flexibility.

---

## 1. Eager Execution

### Overview

* **Default mode in TensorFlow 2.x**
* Operations are **evaluated immediately** as they are called (imperative style).
* More intuitive and Pythonic.

### Characteristics

| Feature           | Description                                   |
| ----------------- | --------------------------------------------- |
| Debuggable        | Easy to inspect intermediate results          |
| Dynamic           | Compatible with control flow (e.g., loops)    |
| No compilation    | Direct execution, no intermediate graph       |
| Slower            | Less optimized than static graphs             |
| Easy to prototype | Great for beginners and rapid experimentation |

### Example

```python
import tensorflow as tf

x = tf.constant([2.0])
y = tf.constant([3.0])
z = x * y
print(z)  # Outputs immediately
```

---

## 2. Graph Execution (tf.function)

### Overview

* Uses **static computation graphs**.
* Achieved in TF 2.x by wrapping functions with `@tf.function`.

### Characteristics

| Feature                                           | Description                                     |
| ------------------------------------------------- | ----------------------------------------------- |
| Optimized                                         | Allows advanced performance optimizations       |
| Portable                                          | Can be serialized and deployed (`SavedModel`)   |
| Static                                            | Control flow becomes part of the graph          |
| Harder to debug                                   | Requires use of `tf.print()` for graph printing |
| Efficient for large-scale training and production |                                                 |

### Example

```python
@tf.function
def multiply(x, y):
    return x * y

result = multiply(tf.constant([2.0]), tf.constant([3.0]))
print(result)  # Executes compiled graph
```

---

## 3. Switching Between Modes

| Context                | Execution Mode |
| ---------------------- | -------------- |
| Plain Python + TF Ops  | Eager          |
| Inside `@tf.function`  | Graph          |
| TensorFlow 1.x default | Graph          |
| TensorFlow 2.x default | Eager          |

To check or set eager execution:

```python
tf.executing_eagerly()  # Returns True/False
```

---

## 4. Trade-offs

| Feature      | Eager Execution      | Graph Execution       |
| ------------ | -------------------- | --------------------- |
| Readability  | High                 | Medium                |
| Debugging    | Easy (Python-native) | Hard (use `tf.print`) |
| Performance  | Lower                | Higher                |
| Portability  | Low                  | High                  |
| Control Flow | Native               | Encoded in graph      |
| Deployment   | Limited              | Preferred             |

---

## 5. Use Cases

| Mode            | Best Use Case                                      |
| --------------- | -------------------------------------------------- |
| Eager Execution | Research, debugging, prototyping                   |
| Graph Execution | Deployment, large-scale training, production usage |

---

## Summary

* **Eager Execution**: Great for development, less optimized.
* **Graph Execution (`@tf.function`)**: Preferred for production and speed.
* TensorFlow 2.x **encourages a mix**: develop eagerly, deploy with graphs.
