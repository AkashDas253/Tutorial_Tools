## Built-in Loss Function

### **Comprehensive Guide to Loss Functions in TensorFlow/Keras**  

Loss functions measure the difference between the predicted output of a model and the actual target values. In TensorFlow/Keras, loss functions are crucial for training models as they guide optimization algorithms in adjusting weights. Below is a categorized and detailed reference for loss functions, their syntax, parameters, and usage.

---

### **Categorized List of Loss Functions**

#### **1. Regression Losses**
| **Loss Function**       | **Description**                                                                                          | **Key Parameters**                                                                                         | **Syntax**                                           | **Example**                                   |
|--------------------------|----------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|----------------------------------------------------|-----------------------------------------------|
| **Mean Squared Error (MSE)** | Measures the average squared difference between predictions and actual values.                        | None                                                                                                      | `'mean_squared_error'` or `tf.keras.losses.MeanSquaredError()` | `loss='mean_squared_error'`                  |
| **Mean Absolute Error (MAE)** | Measures the average absolute difference between predictions and actual values.                      | None                                                                                                      | `'mean_absolute_error'` or `tf.keras.losses.MeanAbsoluteError()` | `loss='mean_absolute_error'`                 |
| **Mean Absolute Percentage Error (MAPE)** | Measures the percentage difference between predicted and actual values.                                  | None                                                                                                      | `'mean_absolute_percentage_error'` or `tf.keras.losses.MeanAbsolutePercentageError()` | `loss='mean_absolute_percentage_error'`      |
| **Huber Loss**           | Combines MSE and MAE for better performance on data with outliers.                                       | `delta` (float): Threshold to switch from squared error to absolute error (`1.0`).                         | `tf.keras.losses.Huber(delta=1.0)`                 | `loss=tf.keras.losses.Huber(delta=1.0)`      |
| **Log-Cosh Loss**        | Smoothed version of MAE, less sensitive to outliers.                                                    | None                                                                                                      | `tf.keras.losses.LogCosh()`                        | `loss=tf.keras.losses.LogCosh()`             |

---

#### **2. Classification Losses**
| **Loss Function**          | **Description**                                                                                      | **Key Parameters**                                                                                  | **Syntax**                                   | **Example**                                     |
|-----------------------------|------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------|----------------------------------------------|-------------------------------------------------|
| **Binary Crossentropy**     | Used for binary classification problems.                                                            | `from_logits` (bool): If predictions are unscaled logits (`False`).                                 | `'binary_crossentropy'` or `tf.keras.losses.BinaryCrossentropy(from_logits=False)` | `loss='binary_crossentropy'`                   |
| **Categorical Crossentropy**| Used for multi-class classification when labels are one-hot encoded.                                | `from_logits` (bool): If predictions are unscaled logits (`False`).                                 | `'categorical_crossentropy'` or `tf.keras.losses.CategoricalCrossentropy(from_logits=False)` | `loss='categorical_crossentropy'`             |
| **Sparse Categorical Crossentropy** | Used for multi-class classification when labels are integers instead of one-hot encoded.                   | `from_logits` (bool): If predictions are unscaled logits (`False`).                                 | `'sparse_categorical_crossentropy'` or `tf.keras.losses.SparseCategoricalCrossentropy(from_logits=False)` | `loss='sparse_categorical_crossentropy'`       |
| **Kullback-Leibler Divergence (KL Divergence)** | Measures the difference between two probability distributions.                                       | None                                                                                                | `tf.keras.losses.KLDivergence()`             | `loss=tf.keras.losses.KLDivergence()`          |
| **Hinge Loss**             | Used for "maximum-margin" classification tasks such as Support Vector Machines (SVM).               | None                                                                                                | `'hinge'` or `tf.keras.losses.Hinge()`       | `loss='hinge'`                                 |
| **Squared Hinge Loss**     | Variation of hinge loss that squares the hinge loss value.                                           | None                                                                                                | `'squared_hinge'` or `tf.keras.losses.SquaredHinge()` | `loss='squared_hinge'`                       |

---

#### **3. Probabilistic Losses**
| **Loss Function**         | **Description**                                                                                      | **Key Parameters**                                  | **Syntax**                                   | **Example**                                   |
|---------------------------|------------------------------------------------------------------------------------------------------|---------------------------------------------------|----------------------------------------------|-----------------------------------------------|
| **Poisson Loss**          | Measures the distance between true and predicted distributions in count data problems.               | None                                              | `'poisson'` or `tf.keras.losses.Poisson()`  | `loss='poisson'`                              |
| **Cosine Similarity**     | Measures the cosine distance between predicted and actual vectors.                                   | `axis` (int): Axis to compute similarity over (`-1`). | `'cosine_similarity'` or `tf.keras.losses.CosineSimilarity(axis=-1)` | `loss='cosine_similarity'`                   |

---

#### **4. Custom Loss Functions**
TensorFlow/Keras allows defining **custom loss functions** to handle unique requirements.

##### Example: Custom Loss Function
```python
import tensorflow as tf

# Custom loss: Mean Squared Logarithmic Error (MSLE)
def custom_msle(y_true, y_pred):
    return tf.reduce_mean(tf.square(tf.math.log1p(y_true) - tf.math.log1p(y_pred)))

# Use in model
model.compile(optimizer='adam', loss=custom_msle)
```

---

### **Choosing a Loss Function**
| **Type of Task**             | **Recommended Loss Functions**                                |
|------------------------------|-------------------------------------------------------------|
| **Regression**               | MSE, MAE, Huber, Log-Cosh                                   |
| **Binary Classification**    | Binary Crossentropy                                         |
| **Multi-class Classification** | Categorical Crossentropy, Sparse Categorical Crossentropy |
| **Probability Distributions**| KLDivergence, Poisson                                      |

---

### **Custom Loss Functions in TensorFlow/Keras**

TensorFlow/Keras allows you to define **custom loss functions** for specific use cases that are not covered by standard loss functions. You can implement custom loss functions by using standard TensorFlow operations or creating more complex formulas. Below is a detailed guide to creating and using custom loss functions, their syntax, and examples.

---

### **Creating Custom Loss Functions**

#### **Basic Structure**
A custom loss function must accept two arguments:
- `y_true`: The true labels.
- `y_pred`: The predicted labels.

The loss function should return a scalar tensor representing the computed loss.

| **Syntax**                    | **Parameters**                                     | **Description**                                                                                           |
|-------------------------------|---------------------------------------------------|-----------------------------------------------------------------------------------------------------------|
| `def custom_loss(y_true, y_pred):` | `y_true` (Tensor): Ground truth values. <br> `y_pred` (Tensor): Predicted values. | A function that computes and returns a scalar loss value.                                                   |

##### Example:
```python
import tensorflow as tf

# Custom Mean Squared Error Loss
def custom_mse(y_true, y_pred):
    return tf.reduce_mean(tf.square(y_true - y_pred))  # Mean squared error

# Use in model
model.compile(optimizer='adam', loss=custom_mse)
```

---

### **Using TensorFlow/Keras Built-in Operations in Custom Loss Functions**
You can use TensorFlow's built-in functions for advanced loss calculations.

#### **Example with `tf.reduce_sum()`**
```python
import tensorflow as tf

# Custom loss using sum of squared errors
def custom_loss_sum(y_true, y_pred):
    return tf.reduce_sum(tf.square(y_true - y_pred))  # Sum of squared errors

model.compile(optimizer='adam', loss=custom_loss_sum)
```

---

## Custom Loss Function

### **Common Custom Loss Functions Examples**

#### 1. **Mean Absolute Error (MAE)**
```python
def custom_mae(y_true, y_pred):
    return tf.reduce_mean(tf.abs(y_true - y_pred))  # Mean absolute error

# Use in model
model.compile(optimizer='adam', loss=custom_mae)
```

#### 2. **Mean Squared Logarithmic Error (MSLE)**
```python
def custom_msle(y_true, y_pred):
    return tf.reduce_mean(tf.square(tf.math.log1p(y_true) - tf.math.log1p(y_pred)))  # MSLE

model.compile(optimizer='adam', loss=custom_msle)
```

#### 3. **Huber Loss (Custom)**
```python
def custom_huber(y_true, y_pred, delta=1.0):
    error = y_true - y_pred
    is_small_error = tf.abs(error) <= delta
    small_error_loss = 0.5 * tf.square(error)
    large_error_loss = delta * (tf.abs(error) - 0.5 * delta)
    return tf.where(is_small_error, small_error_loss, large_error_loss)

# Use in model
model.compile(optimizer='adam', loss=custom_huber)
```

---

### **Advanced Example: Custom Loss with Regularization**
You can combine a custom loss with a regularization term to add penalties to the model's weights.

```python
def custom_loss_with_regularization(y_true, y_pred, model, lambda_reg=0.01):
    # Compute loss (e.g., MSE)
    mse_loss = tf.reduce_mean(tf.square(y_true - y_pred))
    
    # Add L2 regularization (sum of squares of weights)
    reg_loss = lambda_reg * tf.reduce_sum([tf.reduce_sum(tf.square(w)) for w in model.trainable_weights])
    
    return mse_loss + reg_loss

# Use in model
model.compile(optimizer='adam', loss=lambda y_true, y_pred: custom_loss_with_regularization(y_true, y_pred, model))
```

---

### **Custom Loss with Multiple Outputs**
In some models, you may have multiple outputs (e.g., multi-task learning). You can compute different losses for each output and combine them.

```python
def custom_multi_output_loss(y_true, y_pred):
    # For output 1: MSE
    output1_loss = tf.reduce_mean(tf.square(y_true[0] - y_pred[0]))
    
    # For output 2: MAE
    output2_loss = tf.reduce_mean(tf.abs(y_true[1] - y_pred[1]))
    
    return output1_loss + output2_loss

# Use in model
model.compile(optimizer='adam', loss=custom_multi_output_loss)
```

---

### **Loss Functions with Different Input Shapes**
If you need to handle inputs of different shapes, you can reshape tensors inside the loss function.

```python
def custom_loss_with_reshape(y_true, y_pred):
    # Reshape y_true and y_pred to have the same shape
    y_true = tf.reshape(y_true, [-1])
    y_pred = tf.reshape(y_pred, [-1])
    
    # Compute custom loss (e.g., Mean Squared Error)
    return tf.reduce_mean(tf.square(y_true - y_pred))

# Use in model
model.compile(optimizer='adam', loss=custom_loss_with_reshape)
```

---

### **Using Custom Loss in Training**

After defining a custom loss function, you can use it directly in the `model.compile()` method by passing it as the `loss` parameter.

| **Syntax**                   | **Description**                                 |
|------------------------------|-------------------------------------------------|
| `model.compile(optimizer, loss=custom_loss)` | Pass the custom loss function when compiling the model. |

Example:
```python
model.compile(optimizer='adam', loss=custom_loss)
```

---

### **Key Points to Remember**
- Custom loss functions in TensorFlow/Keras are written as Python functions that accept `y_true` and `y_pred` tensors.
- The loss function should return a scalar tensor.
- You can use TensorFlow operations such as `tf.reduce_mean()`, `tf.square()`, `tf.abs()`, etc., to compute the loss.
- Regularization terms, multi-output losses, and reshaping of tensors are all possible within custom loss functions.

This guide gives you a flexible and powerful way to define custom loss functions suited to specific problems and architectures.