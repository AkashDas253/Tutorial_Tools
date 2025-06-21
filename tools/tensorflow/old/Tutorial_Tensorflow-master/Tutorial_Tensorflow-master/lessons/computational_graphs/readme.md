## **Computational Graphs in TensorFlow**  

### **Overview**  
A **computational graph** in TensorFlow represents mathematical operations as a directed acyclic graph (DAG). Nodes represent **operations (ops)**, and edges represent **data flow (tensors)** between them. TensorFlow supports two execution modes:  

- **Eager Execution** (default) – Executes operations immediately.  
- **Graph Execution** – Uses `tf.function` to compile operations into a computational graph for efficiency.  

---

## **1. Key Components of Computational Graphs**  

| **Component**  | **Description** |
|--------------|----------------|
| **Operations (Ops)** | Nodes representing mathematical operations. |
| **Tensors** | Data flowing between operations. |
| **Variables** | Trainable parameters stored in memory. |
| **Constants** | Immutable values used in computations. |
| **Placeholders (TF1.x only)** | Input values provided at runtime. |
| **tf.function** | Converts Python functions into computational graphs for efficiency. |

---

## **2. Creating a Computational Graph in TensorFlow**  

### **A. Basic Computational Graph**  
```python
import tensorflow as tf

# Define operations
x = tf.constant(5.0)
y = tf.constant(3.0)
z = x * y + y  # TensorFlow automatically builds a computation graph

print(z)  # Eager execution prints result immediately
```

---

### **B. Using `tf.function` to Create a Graph**  
```python
@tf.function
def compute(x, y):
    return x * y + y  # Converted to a computational graph

x = tf.constant(5.0)
y = tf.constant(3.0)
print(compute(x, y))  # Executes in graph mode
```
- `tf.function` **optimizes execution** by compiling into a graph.  
- **Speeds up training** by avoiding redundant Python execution overhead.  

---

## **3. Viewing Computational Graphs Using TensorBoard**  

### **A. Enable Logging**  
```python
writer = tf.summary.create_file_writer("logs")

@tf.function
def graph_function(x, y):
    return x * y + y

x = tf.constant(2.0)
y = tf.constant(3.0)

# Log computation graph
with writer.as_default():
    tf.summary.trace_on(graph=True, profiler=True)
    result = graph_function(x, y)
    tf.summary.trace_export(name="my_graph", step=0)
```
### **B. Run TensorBoard**
```bash
tensorboard --logdir=logs
```
- **TensorBoard** visualizes computation graphs for debugging.  

---

## **4. Benefits of Using Computational Graphs**  
| **Advantage** | **Description** |
|--------------|----------------|
| **Performance** | Graphs optimize execution by fusing operations. |
| **Portability** | Graphs can be saved, loaded, and deployed independently. |
| **Auto-Differentiation** | TensorFlow efficiently computes gradients for optimization. |
| **Device Optimization** | Graphs execute efficiently on CPU, GPU, and TPU. |

---

## **5. Summary**  
- **Computational graphs structure operations** in TensorFlow.  
- **Eager Execution is default**, but `tf.function` enables **graph execution** for efficiency.  
- **TensorBoard helps visualize graphs** for debugging.  
- **Graph-based execution improves performance** by reducing redundant computations.  