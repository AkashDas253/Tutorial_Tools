# Model Serialization

---

## What Is Model Serialization?

**Model serialization** is the process of **saving a model’s architecture, weights, training configuration, and optimizer state** to disk so it can be:

* **Reloaded** later for inference or continued training.
* **Shared** or **deployed** in production or across platforms.

---

## Core Serialization Options

| Method                | Format                | Includes            | Use Case                           |
| --------------------- | --------------------- | ------------------- | ---------------------------------- |
| `SavedModel`          | Directory (`pb`)      | ✅ All               | Recommended; deployment & reuse    |
| `HDF5 (.h5)`          | Single file           | ✅ All               | Keras-compatible legacy format     |
| `JSON/YAML + Weights` | `.json/.yaml` + `.h5` | ❌ Only architecture | For transferring architecture only |

---

## 1. **SavedModel Format (Recommended)**

TensorFlow’s default format for full serialization.
Saves:

* Model architecture
* Trained weights
* Optimizer config
* Training state (metrics, loss)

### Save

```python
model.save("saved_model_dir")  # folder format
```

### Load

```python
model = tf.keras.models.load_model("saved_model_dir")
```

---

## 2. **HDF5 Format (`.h5`)**

Keras-compatible file. Good for portability with other Keras-based tools.

### Save

```python
model.save("model.h5")
```

### Load

```python
model = tf.keras.models.load_model("model.h5")
```

---

## 3. **Saving Only Weights**

Use when you want to reuse weights in a different model instance.

### Save

```python
model.save_weights("weights.h5")
```

### Load

```python
model.load_weights("weights.h5")
```

---

## 4. **Saving Architecture Only**

### JSON

```python
# Save
json_config = model.to_json()
with open("model.json", "w") as f:
    f.write(json_config)

# Load
from tensorflow.keras.models import model_from_json
with open("model.json") as f:
    model = model_from_json(f.read())
```

### YAML

```python
# Save
yaml_config = model.to_yaml()

# Load
from tensorflow.keras.models import model_from_yaml
model = model_from_yaml(yaml_config)
```

> **Note**: YAML support may require enabling in some environments.

---

## 5. **Serialize Custom Layers or Models**

If you define custom objects, include them during deserialization:

```python
model.save('custom_model.h5')

model = tf.keras.models.load_model(
    'custom_model.h5',
    custom_objects={'CustomLayer': CustomLayer}
)
```

---

## 6. **Version Control**

You can save versions as subfolders:

```
models/
  my_model/
    1/
      saved_model.pb
      variables/
    2/
      saved_model.pb
```

Useful with **TensorFlow Serving**.

---

## 7. **Serialization in `tf.train.Checkpoint` (Advanced)**

Alternative method to serialize arbitrary objects.

### Save

```python
ckpt = tf.train.Checkpoint(model=model, optimizer=optimizer)
ckpt.save('checkpoint/my_ckpt')
```

### Load

```python
ckpt = tf.train.Checkpoint(model=model, optimizer=optimizer)
ckpt.restore(tf.train.latest_checkpoint('checkpoint/'))
```

---

## Comparison Table

| Format          | Saves Weights  | Saves Architecture | Saves Optimizer | Use in Serving | Portability |
| --------------- | -------------- | ------------------ | --------------- | -------------- | ----------- |
| `SavedModel`    | ✅              | ✅                  | ✅               | ✅              | ✅           |
| `.h5` (HDF5)    | ✅              | ✅                  | ✅               | ❌              | ✅           |
| `.json` + `.h5` | ✅ (separately) | ✅                  | ❌               | ❌              | ✅           |
| `Checkpoint`    | ✅              | ❌ (manual)         | ✅               | ❌              | ✅           |

---

## Best Practices

* Use **`SavedModel`** for production, serving, and cross-platform use.
* Use `.h5` for quick experiments or legacy tools.
* Always save both architecture and weights unless transferring across designs.
* Use `custom_objects` when loading models with custom layers or losses.
* Use `Checkpoint` for **low-level control** and checkpointing in custom training loops.

---
