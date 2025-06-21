# Data Handling

---

## Core Objectives

TensorFlow provides **efficient, scalable, and flexible** tools for preparing, loading, and feeding data into machine learning models. The main components include:

* `tf.data` API
* `tf.keras.utils`
* `tf.io` for I/O operations
* `tf.feature_column` for structured data
* Dataset wrappers for CSV, TFRecord, image, text

---

## `tf.data` API: Input Pipeline Framework

### Purpose

Build efficient, scalable pipelines to load, transform, and feed data.

### Key Concepts

| Operation            | Description                                |
| -------------------- | ------------------------------------------ |
| `from_tensor_slices` | Converts in-memory tensors into a dataset  |
| `from_generator`     | Wraps a Python generator                   |
| `from_list_files`    | Reads a list of files                      |
| `interleave`         | Reads files in parallel                    |
| `map`                | Applies transformation to each element     |
| `shuffle`            | Randomizes input order                     |
| `batch`              | Groups elements into batches               |
| `repeat`             | Repeats dataset (infinite or fixed)        |
| `prefetch`           | Overlaps preprocessing and model execution |
| `cache`              | Caches data to speed up epochs             |

### Example

```python
ds = tf.data.Dataset.from_tensor_slices((features, labels))
ds = ds.shuffle(buffer_size=1000).batch(32).prefetch(tf.data.AUTOTUNE)
```

---

## `tf.keras.utils` Utilities

| Utility                        | Description                                  |
| ------------------------------ | -------------------------------------------- |
| `image_dataset_from_directory` | Loads image datasets from a folder hierarchy |
| `get_file`                     | Downloads files (e.g., datasets) from URL    |
| `to_categorical`               | One-hot encodes class labels                 |
| `normalize`                    | Scales image pixels                          |
| `Sequence`                     | Base class for custom data generators        |

---

## Structured Data Handling

### `tf.feature_column`

Used for preprocessing structured/tabular data before feeding it into models.

| Feature Column Type                       | Use Case                                  |
| ----------------------------------------- | ----------------------------------------- |
| `numeric_column`                          | For continuous numeric features           |
| `categorical_column_with_vocabulary_list` | For known categorical values              |
| `embedding_column`                        | For high-cardinality categorical features |
| `bucketized_column`                       | For binning numeric features              |
| `crossed_column`                          | For feature interactions                  |

> Note: Feature columns are being phased out in favor of Keras preprocessing layers.

---

## Keras Preprocessing Layers (Preferred)

| Layer               | Description                                          |
| ------------------- | ---------------------------------------------------- |
| `Normalization`     | Standardizes numeric input                           |
| `CategoryEncoding`  | One-hot or multi-hot encoding                        |
| `StringLookup`      | Converts strings to integer indices                  |
| `IntegerLookup`     | Converts integers to dense or sparse representations |
| `TextVectorization` | Tokenizes and processes text                         |
| `Discretization`    | Buckets numeric values                               |

### Example

```python
normalizer = tf.keras.layers.Normalization()
normalizer.adapt(data)
```

---

## Image Data Handling

| Method                                      | Description                                   |
| ------------------------------------------- | --------------------------------------------- |
| `image_dataset_from_directory()`            | Load labeled image dataset from folders       |
| `tf.io.read_file()` + `tf.image.decode_*()` | Custom image loading                          |
| `tf.image.*`                                | Image preprocessing: resize, crop, flip, etc. |

---

## Text Data Handling

| Tool                 | Description                           |
| -------------------- | ------------------------------------- |
| `TextVectorization`  | Built-in Keras layer for tokenization |
| `Tokenizer` (legacy) | Old Keras tokenization utility        |
| `tf.strings`         | Low-level string operations           |

---

## Time Series / Sequence Data Handling

* Use sliding windows via `Dataset.window()`, `Dataset.flat_map()`
* Example structure:

  ```python
  dataset = tf.data.Dataset.range(100)
  dataset = dataset.window(10, shift=1).flat_map(lambda x: x.batch(10))
  ```

---

## Working with TFRecord Format

* **Binary record format** for efficient serialization and I/O
* Especially useful in large-scale distributed training

### Key APIs

* `tf.io.TFRecordWriter` to write
* `tf.data.TFRecordDataset` to read
* `tf.train.Example` for encoding data

---

## CSV and Text Handling

| API                  | Description                           |
| -------------------- | ------------------------------------- |
| `make_csv_dataset()` | Load CSV files directly into datasets |
| `decode_csv()`       | Parse CSV line into tensors           |
| `TextLineDataset()`  | Reads text files line-by-line         |

---

## Shuffling, Batching, Prefetching

| Operation    | Purpose                          |
| ------------ | -------------------------------- |
| `shuffle()`  | Randomizes data order            |
| `batch()`    | Combines examples into batches   |
| `prefetch()` | Optimizes input pipeline latency |

Example:

```python
dataset = dataset.shuffle(1000).batch(32).prefetch(tf.data.AUTOTUNE)
```

---

## Performance Optimization Tips

* Use `AUTOTUNE` to automatically tune buffer sizes
* Cache static datasets using `.cache()`
* Use `.prefetch()` to overlap data prep and training
* Store large datasets in `TFRecord` format
* Use vectorized operations in `map()`

---

## Summary Table

| Task                 | Recommended Tool                         |
| -------------------- | ---------------------------------------- |
| Load in-memory data  | `from_tensor_slices`, `from_generator`   |
| Load image datasets  | `image_dataset_from_directory`           |
| Load structured data | `make_csv_dataset`, feature columns      |
| Tokenize text        | `TextVectorization`                      |
| Optimize pipeline    | `shuffle`, `batch`, `prefetch`, `cache`  |
| Handle massive data  | `TFRecord`, `interleave`, `parallel_map` |

---
