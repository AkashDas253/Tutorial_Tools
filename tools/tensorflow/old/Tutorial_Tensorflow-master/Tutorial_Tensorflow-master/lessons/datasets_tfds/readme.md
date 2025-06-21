## **TensorFlow Datasets (TFDS)**  

### **Overview**  
TensorFlow Datasets (**TFDS**) is a **collection of ready-to-use datasets** for machine learning and deep learning tasks. It provides datasets in **TensorFlow (TF) format**, making it easier to load and preprocess data.  

---

### **Key Features**  

| **Feature**        | **Description** |
|------------------|----------------------------------------------|
| Ready-to-use datasets | Provides datasets for images, text, audio, and more. |
| Automatic downloading | Downloads and caches datasets automatically. |
| Works with TensorFlow | Provides datasets as `tf.data.Dataset` objects. |
| Supports different splits | Allows train/test/validation splits. |

---

### **Installing TFDS**  
```bash
pip install tensorflow-datasets
```

---

### **Loading a Dataset**  
```python
import tensorflow_datasets as tfds

# Load the MNIST dataset
dataset, info = tfds.load('mnist', split='train', with_info=True, as_supervised=True)

# Print dataset information
print(info)
```

- `split='train'`: Loads the training set.  
- `with_info=True`: Returns metadata like dataset size, features, etc.  
- `as_supervised=True`: Returns `(features, labels)` instead of a dictionary.  

---

### **Available Datasets in TFDS**  

| **Category** | **Example Datasets** |
|-------------|----------------------|
| Images | MNIST, CIFAR-10, ImageNet |
| Text | IMDB Reviews, Wikipedia, GLUE |
| Audio | SpeechCommands, LibriSpeech |
| Video | Kinetics-700, Moving MNIST |
| Graphs | OGB, ZINC |
| Reinforcement Learning | Atari, DMLab |

To list all available datasets:  
```python
print(tfds.list_builders())
```

---

### **Dataset Splitting**  
TFDS supports different dataset splits:  

| **Split** | **Usage** |
|----------|------------------|
| `train` | Training data |
| `test` | Testing data |
| `validation` | Validation data |
| `train[:80%]` | First 80% of training data |
| `train[80%:]` | Last 20% of training data |

Example: Load **80% train, 20% test**  
```python
train_data = tfds.load('mnist', split='train[:80%]')
test_data = tfds.load('mnist', split='train[80%:]')
```

---

### **Preprocessing TFDS Data**  
TFDS returns data as **TensorFlow datasets (`tf.data.Dataset`)**, which can be preprocessed using `map()`.  

```python
import tensorflow as tf

# Normalize images to [0,1] range
def normalize_img(image, label):
    image = tf.cast(image, tf.float32) / 255.0
    return image, label

# Load and preprocess MNIST dataset
dataset = tfds.load('mnist', split='train', as_supervised=True)
dataset = dataset.map(normalize_img).batch(32)
```

---

### **Converting TFDS Data to NumPy**  
```python
for image, label in tfds.as_numpy(dataset):
    print(image.shape, label)
    break
```

---

### **Dataset Caching and Prefetching**  
To improve performance:  
```python
dataset = dataset.cache().shuffle(1000).prefetch(tf.data.AUTOTUNE)
```

| **Optimization** | **Description** |
|-----------------|----------------|
| `cache()` | Caches data in memory/disk for faster access. |
| `shuffle(1000)` | Randomizes dataset order. |
| `prefetch(AUTOTUNE)` | Overlaps data loading with model training. |

---

### **Use Cases**  

| **Task** | **Should You Use TFDS?** |
|---------|---------------------------|
| Quick access to datasets | ✅ Yes, provides ready-to-use datasets. |
| Custom datasets | ❌ No, use `tf.data.Dataset.from_tensor_slices()`. |
| Large-scale datasets | ✅ Yes, supports streaming datasets. |
| Specialized datasets | ❌ No, might not include your dataset. |

---

### **Conclusion**  
- **TFDS simplifies dataset loading** by providing prebuilt datasets in TensorFlow format.  
- It **automates downloading, splitting, and preprocessing**, improving efficiency.  
- Ideal for quick prototyping, but **custom datasets** require `tf.data` pipelines.