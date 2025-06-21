## **TensorFlow Feature Column API**

The **Feature Column** API in TensorFlow is a powerful tool used to handle and transform input data into a format that can be fed into machine learning models, particularly when working with **structured data** (e.g., CSV files, dataframes). Feature columns are an abstraction layer that help TensorFlow understand how to treat raw input data and how to prepare it for training or evaluation.

Feature columns are used to define the transformations required to preprocess the input features, such as scaling, encoding, or transforming categorical features. Once defined, feature columns can be passed to the model for training.

---

### **Key Types of Feature Columns**

| **Feature Column Type**        | **Description**                                                                                                     | **Example**                                                                                     |
|---------------------------------|---------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
| **`NumericColumn`**             | Represents continuous numeric features. These features are passed directly into the model.                        | `numeric_feature = tf.feature_column.numeric_column(key="feature_name")`                      |
| **`CategoricalColumn`**         | Represents categorical features. Can be used to encode features as one-hot vectors or embeddings.                  | `categorical_column = tf.feature_column.categorical_column_with_vocabulary_list("category", ["A", "B", "C"])` |
| **`EmbeddingColumn`**           | Represents categorical features that are encoded as embeddings. These are typically used for large cardinality features. | `embedding_column = tf.feature_column.embedding_column(categorical_column, dimension=8)`       |
| **`BucketizedColumn`**          | Represents a continuous numeric feature divided into buckets (e.g., for age ranges).                               | `bucketized_column = tf.feature_column.bucketized_column(numeric_column, boundaries=[18, 25, 35])` |
| **`CrossedColumn`**             | Represents a combination of multiple features (e.g., the interaction between two features).                         | `crossed_column = tf.feature_column.crossed_column([feature_1, feature_2], hash_bucket_size=1000)` |
| **`IndicatorColumn`**           | Converts categorical data into a sparse one-hot encoded tensor. Typically used with categorical features.            | `indicator_column = tf.feature_column.indicator_column(categorical_column)`                    |
| **`WeightedSumColumn`**         | Represents weighted features, where each feature has an associated weight that indicates its importance.             | `weighted_column = tf.feature_column.weighted_sum_column(numeric_column, weight_column)`      |

---

### **Feature Columns and Their Parameters**

| **Feature Column**                | **Parameter(s)**                                                | **Description**                                                                                      | **Example**                                                                                              |
|-----------------------------------|---------------------------------------------------------------|------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| **`numeric_column`**              | `key`                                                          | The name of the feature.                                                                                | `numeric_feature = tf.feature_column.numeric_column(key="feature_name")`                                |
|                                   | `dtype`                                                        | The data type of the feature (default is `tf.float32`).                                                  | `numeric_feature = tf.feature_column.numeric_column(key="feature_name", dtype=tf.float64)`             |
| **`categorical_column_with_vocabulary_list`** | `key`                                                          | The name of the feature.                                                                                | `categorical_column = tf.feature_column.categorical_column_with_vocabulary_list("category", ["A", "B", "C"])` |
|                                   | `vocabulary_list`                                              | The list of possible categories.                                                                         | `categorical_column = tf.feature_column.categorical_column_with_vocabulary_list("category", ["A", "B", "C"])` |
|                                   | `dtype`                                                        | The data type of the feature (default is `tf.string`).                                                  | `categorical_column = tf.feature_column.categorical_column_with_vocabulary_list("category", ["A", "B", "C"], dtype=tf.int32)` |
| **`embedding_column`**            | `categorical_column`                                           | The categorical column to be embedded.                                                                  | `embedding_column = tf.feature_column.embedding_column(categorical_column, dimension=8)`               |
|                                   | `dimension`                                                    | The dimension of the embedding.                                                                         | `embedding_column = tf.feature_column.embedding_column(categorical_column, dimension=8)`               |
|                                   | `combiner`                                                     | Combiner function for the embedding (default is 'sum').                                                 | `embedding_column = tf.feature_column.embedding_column(categorical_column, dimension=8, combiner='mean')` |
| **`bucketized_column`**           | `source_column`                                                | The continuous numeric column that will be bucketized.                                                  | `bucketized_column = tf.feature_column.bucketized_column(numeric_column, boundaries=[18, 25, 35])`      |
|                                   | `boundaries`                                                   | A list of bucket boundaries.                                                                             | `bucketized_column = tf.feature_column.bucketized_column(numeric_column, boundaries=[18, 25, 35])`      |
| **`crossed_column`**              | `column1, column2,...`                                          | A list of feature columns to combine (cross).                                                           | `crossed_column = tf.feature_column.crossed_column([feature_1, feature_2], hash_bucket_size=1000)`      |
|                                   | `hash_bucket_size`                                             | The size of the hash table for cross-product columns.                                                   | `crossed_column = tf.feature_column.crossed_column([feature_1, feature_2], hash_bucket_size=1000)`      |
| **`indicator_column`**            | `categorical_column`                                           | The categorical column to be converted to an indicator (one-hot) column.                               | `indicator_column = tf.feature_column.indicator_column(categorical_column)`                           |
| **`weighted_sum_column`**        | `column`                                                       | The column whose weighted sum is being calculated.                                                      | `weighted_column = tf.feature_column.weighted_sum_column(numeric_column, weight_column)`              |
|                                   | `weight_column`                                                | The column representing the weights associated with each feature.                                      | `weighted_column = tf.feature_column.weighted_sum_column(numeric_column, weight_column)`              |

---

### **How to Use Feature Columns**

1. **Define Feature Columns**: Feature columns are defined to transform raw input features into formats suitable for model training.
   
```python
import tensorflow as tf

# Define numeric feature columns
numeric_feature = tf.feature_column.numeric_column(key="feature_name")

# Define categorical feature column with a list of possible values
categorical_feature = tf.feature_column.categorical_column_with_vocabulary_list(
    key="category", vocabulary_list=["A", "B", "C"]
)

# Create embedding column for categorical feature
embedding_column = tf.feature_column.embedding_column(categorical_feature, dimension=8)

# Bucketize a continuous feature
bucketized_column = tf.feature_column.bucketized_column(numeric_feature, boundaries=[18, 25, 35])

# Cross two columns
crossed_column = tf.feature_column.crossed_column([numeric_feature, categorical_feature], hash_bucket_size=1000)
```

2. **Using Feature Columns in the Model**: Once feature columns are defined, they are passed to the `input_layer` to create a model's input layer.

```python
# Example: Create a DNN model with feature columns
feature_columns = [numeric_feature, embedding_column, bucketized_column, crossed_column]

# Build the model
input_layer = tf.feature_column.input_layer(features, feature_columns)

# Add dense layers
net = tf.compat.v1.layers.dense(input_layer, units=128, activation=tf.nn.relu)
net = tf.compat.v1.layers.dense(net, units=1, activation=None)
```

3. **Feature Columns in `input_fn`**: You can pass the feature columns in an `input_fn` that provides the data to the model.

```python
# Define the input function
def input_fn():
    dataset = tf.data.Dataset.from_tensor_slices((features, labels))
    dataset = dataset.batch(32)
    return dataset

# Train the model using the feature columns
model.train(input_fn=input_fn, steps=1000)
```

---

### **Conclusion**

TensorFlow's **Feature Column** API is a versatile tool for transforming raw input data into a format suitable for machine learning models. Whether you're working with numeric, categorical, or bucketized data, feature columns help you pre-process your data before feeding it into the model. Understanding how to properly use feature columns is critical for building high-quality models, especially when dealing with structured data.

