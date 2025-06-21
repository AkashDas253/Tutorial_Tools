## Data Pipelines in TensorFlow

#### **1. Overview**
Data pipelines in TensorFlow streamline the process of data loading, transformation, and feeding to models. They ensure efficient handling of large datasets and support operations like batching, shuffling, and preprocessing.

---

#### **2. Dataset API**

| **Method**                              | **Description**                                                                                         | **Example**                                                                                 |
|-----------------------------------------|---------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|
| `tf.data.Dataset.from_tensor_slices`    | Creates a dataset from tensor slices.                                                                  | `dataset = tf.data.Dataset.from_tensor_slices([1, 2, 3])`                                   |
| `tf.data.Dataset.from_generator`        | Creates a dataset from a Python generator function.                                                    | `dataset = tf.data.Dataset.from_generator(gen_func, output_types=tf.int32)`                 |
| `tf.data.Dataset.from_tfrecord`         | Creates a dataset from TFRecord files.                                                                 | `dataset = tf.data.TFRecordDataset("data.tfrecords")`                                       |
| `tf.data.Dataset.list_files`            | Creates a dataset of file paths from a glob pattern.                                                   | `dataset = tf.data.Dataset.list_files("images/*.jpg")`                                      |
| `tf.data.experimental.load`             | Loads a previously saved dataset.                                                                      | `dataset = tf.data.experimental.load("saved_dataset")`                                      |

---

#### **3. Dataset Transformations**

| **Transformation** | **Description**                                                                                          | **Example**                                                                                                  |
|---------------------|----------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| `map`              | Applies a function to each element in the dataset.                                                       | `dataset = dataset.map(lambda x: x * 2)`                                                                    |
| `filter`           | Filters elements based on a condition.                                                                   | `dataset = dataset.filter(lambda x: x % 2 == 0)`                                                            |
| `batch`            | Combines consecutive elements into batches.                                                              | `dataset = dataset.batch(32)`                                                                               |
| `shuffle`          | Randomly shuffles elements.                                                                              | `dataset = dataset.shuffle(buffer_size=100)`                                                                |
| `cache`            | Caches the dataset in memory/disk to improve performance.                                                | `dataset = dataset.cache()`                                                                                 |
| `prefetch`         | Preloads elements for efficient data consumption during training.                                         | `dataset = dataset.prefetch(tf.data.AUTOTUNE)`                                                              |
| `zip`              | Combines multiple datasets into one.                                                                     | `dataset = tf.data.Dataset.zip((dataset1, dataset2))`                                                       |

---

#### **4. TFRecord Format**
The **TFRecord** format is a lightweight and efficient binary file format optimized for TensorFlow.

| **Step**             | **Description**                              | **Example**                                                                                     |
|-----------------------|----------------------------------------------|-------------------------------------------------------------------------------------------------|
| **Writing TFRecords** | Serialize data and write it to `.tfrecords`. | ```python<br>with tf.io.TFRecordWriter('file.tfrecords') as writer: writer.write(serialized)``` |
| **Reading TFRecords** | Parse TFRecord files during data loading.    | `dataset = tf.data.TFRecordDataset("file.tfrecords")`                                           |

---

#### **5. Data Augmentation**
TensorFlow provides tools for data augmentation, especially for images and text.

| **Augmentation Type**       | **Function**                              | **Example**                                                      |
|-----------------------------|-------------------------------------------|------------------------------------------------------------------|
| **Image Rotation**          | `tf.image.rot90`                         | `tf.image.rot90(image, k=1)`                                    |
| **Flipping**                | `tf.image.flip_left_right` or `tf.image.flip_up_down` | `tf.image.flip_left_right(image)`                    |
| **Resizing**                | `tf.image.resize`                        | `tf.image.resize(image, [224, 224])`                            |
| **Normalization**           | `tf.image.per_image_standardization`     | `tf.image.per_image_standardization(image)`                     |
| **Text Tokenization**       | `tf.keras.preprocessing.text.Tokenizer`  | `tokenizer.fit_on_texts(corpus)`                                |

---

#### **6. Combining Pipelines**
Efficient pipelines often combine multiple transformations:

```python
import tensorflow as tf

# Load data
dataset = tf.data.Dataset.from_tensor_slices([1, 2, 3, 4, 5])

# Transformations
dataset = (dataset
           .map(lambda x: x * 2)         # Multiply elements by 2
           .filter(lambda x: x > 5)      # Filter elements > 5
           .batch(2)                     # Batch elements into groups of 2
           .prefetch(tf.data.AUTOTUNE))  # Prefetch to improve performance

for batch in dataset:
    print(batch)
```

---

#### **7. Common Use Cases**

| **Scenario**                | **Pipeline Workflow**                                                                                   |
|-----------------------------|---------------------------------------------------------------------------------------------------------|
| **Image Classification**    | Load images -> Resize -> Normalize -> Batch -> Prefetch                                               |
| **Text Classification**     | Load text -> Tokenize -> Pad sequences -> Batch -> Prefetch                                           |
| **Large Dataset Training**  | Load TFRecords -> Parse -> Shuffle -> Batch -> Prefetch                                               |
