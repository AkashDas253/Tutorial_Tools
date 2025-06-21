# Model Building Approaches

---

## Purpose

TensorFlow (via `tf.keras`) offers **three distinct approaches** for building machine learning models. Each offers a different balance between **simplicity, flexibility, and control**.

---

## Overview of Approaches

| Approach          | Description                            | Use Case                               |
| ----------------- | -------------------------------------- | -------------------------------------- |
| Sequential API    | Stack of layers, linear flow           | Simple, feed-forward models            |
| Functional API    | Directed acyclic graph of layers       | Multi-input/output, complex topologies |
| Model Subclassing | Fully custom behavior and architecture | Dynamic models, research prototypes    |

---

## 1. Sequential API

### Description

* Simplest way to build models by stacking layers sequentially.
* One input and one output.

### Syntax

```python
from tensorflow.keras import Sequential, layers

model = Sequential([
    layers.Dense(128, activation='relu', input_shape=(784,)),
    layers.Dense(10, activation='softmax')
])
```

### Limitations

* No support for multiple inputs/outputs
* No layer sharing or non-linear topology

---

## 2. Functional API

### Description

* Layers are treated as functions on tensors.
* Allows branching, merging, shared layers, multiple inputs/outputs.

### Syntax

```python
from tensorflow.keras import Model, Input, layers

inputs = Input(shape=(784,))
x = layers.Dense(128, activation='relu')(inputs)
x = layers.Dropout(0.3)(x)
outputs = layers.Dense(10, activation='softmax')(x)

model = Model(inputs, outputs)
```

### Features

* Can create arbitrary directed acyclic graphs (DAGs)
* More modular and reusable
* Easier to visualize with `model.summary()` and `plot_model()`

---

## 3. Model Subclassing

### Description

* Subclass `tf.keras.Model` and define custom logic in the `call()` method.
* Full control over forward pass and layers.

### Syntax

```python
from tensorflow.keras import Model, layers

class MyModel(Model):
    def __init__(self):
        super(MyModel, self).__init__()
        self.d1 = layers.Dense(128, activation='relu')
        self.d2 = layers.Dense(10, activation='softmax')

    def call(self, inputs):
        x = self.d1(inputs)
        return self.d2(x)

model = MyModel()
```

### Features

* Supports dynamic control flow (`if`, `for`, etc.)
* Ideal for RNNs, conditional branches, and experimentation
* Less introspectable (`model.summary()` may not work until model is called)

---

## Comparison Table

| Feature                   | Sequential | Functional | Subclassing  |
| ------------------------- | ---------- | ---------- | ------------ |
| Simple Models             | Yes        | Yes        | Yes          |
| Complex Topologies        | No         | Yes        | Yes          |
| Multiple Inputs/Outputs   | No         | Yes        | Yes          |
| Custom Training Logic     | Limited    | Moderate   | Full Control |
| Readability               | High       | High       | Medium       |
| Best for Beginners        | Yes        | Yes        | No           |
| Summary and Visualization | Yes        | Yes        | Partially    |

---

## Recommendation by Use Case

| Use Case                          | Suggested Approach        |
| --------------------------------- | ------------------------- |
| Basic feedforward model           | Sequential                |
| Shared layers or complex DAGs     | Functional                |
| Custom control flow (e.g., loops) | Subclassing               |
| Research and experimentation      | Subclassing               |
| Multiple inputs/outputs           | Functional or Subclassing |

---
