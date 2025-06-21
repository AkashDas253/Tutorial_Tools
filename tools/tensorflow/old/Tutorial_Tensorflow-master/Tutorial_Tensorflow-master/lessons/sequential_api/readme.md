## **Sequential API in TensorFlow**  

### **Overview**  
The **Sequential API** in TensorFlow's Keras module provides a simple way to build **neural networks layer by layer**. It is best suited for models where **each layer has exactly one input and one output**.  

---

### **When to Use the Sequential API?**  

| **Use Case** | **Description** |
|-------------|----------------|
| **Linear Stack of Layers** | Model follows a straight path from input to output. |
| **No Multiple Inputs/Outputs** | Supports only a single input and output per layer. |
| **No Complex Layer Connections** | No shared layers, residual connections, or multi-branch architectures. |

---

### **Creating a Model Using `tf.keras.Sequential`**  
```python
import tensorflow as tf

model = tf.keras.Sequential([
    tf.keras.layers.Dense(64, activation='relu', input_shape=(100,)),  # Input Layer
    tf.keras.layers.Dense(32, activation='relu'),  # Hidden Layer
    tf.keras.layers.Dense(10, activation='softmax')  # Output Layer
])
```

---

### **Adding Layers Incrementally**  
You can also build the model step by step using `.add()`:
```python
model = tf.keras.Sequential()
model.add(tf.keras.layers.Dense(64, activation='relu', input_shape=(100,)))
model.add(tf.keras.layers.Dense(32, activation='relu'))
model.add(tf.keras.layers.Dense(10, activation='softmax'))
```

---

### **Configuring the Model**  
Before training, compile the model:
```python
model.compile(optimizer='adam',
              loss='sparse_categorical_crossentropy',
              metrics=['accuracy'])
```

| **Parameter** | **Description** |
|--------------|----------------|
| `optimizer` | Algorithm to update model weights (`adam`, `sgd`, etc.). |
| `loss` | Defines how errors are calculated (`mse`, `categorical_crossentropy`). |
| `metrics` | Performance evaluation (e.g., `accuracy`). |

---

### **Training the Model**  
Use `fit()` to train:
```python
history = model.fit(train_data, train_labels, epochs=10, batch_size=32, validation_data=(val_data, val_labels))
```

| **Parameter** | **Description** |
|--------------|----------------|
| `train_data` | Input features. |
| `train_labels` | Target labels. |
| `epochs` | Number of training iterations. |
| `batch_size` | Number of samples processed at a time. |
| `validation_data` | Data used to evaluate performance. |

---

### **Evaluating and Predicting**  
Evaluate model performance:
```python
loss, accuracy = model.evaluate(test_data, test_labels)
print(f"Test Accuracy: {accuracy}")
```

Make predictions:
```python
predictions = model.predict(new_data)
```

---

### **Summary of Key Functions**  

| **Function** | **Purpose** |
|-------------|------------|
| `tf.keras.Sequential()` | Creates a sequential model. |
| `.add(layer)` | Adds a new layer to the model. |
| `.compile(optimizer, loss, metrics)` | Configures training settings. |
| `.fit(x, y, epochs, batch_size, validation_data)` | Trains the model. |
| `.evaluate(x, y)` | Evaluates model performance. |
| `.predict(x)` | Makes predictions on new data. |

---

### **Limitations of Sequential API**  
- Cannot handle **multiple inputs or outputs**.  
- Does not support **residual connections or custom layer combinations**.  
- Not suitable for **advanced architectures like GANs or Transformers**.  

For complex architectures, use the **Functional API** or **Subclassing API**.