## **Functional API in TensorFlow**  

### **Overview**  
The **Functional API** in TensorFlow provides a flexible way to build **complex neural networks**. Unlike the **Sequential API**, it allows:  
- **Multiple inputs and outputs**  
- **Shared layers**  
- **Residual connections and skip connections**  
- **Graph-based layer definitions**  

---

### **When to Use the Functional API?**  

| **Use Case** | **Description** |
|-------------|----------------|
| **Multiple Inputs/Outputs** | When a model requires multiple inputs or outputs. |
| **Shared Layers** | When a layer needs to be reused (e.g., Siamese networks). |
| **Custom Architectures** | Allows skip connections (ResNet), multi-branch networks, etc. |
| **More Flexibility** | Provides better control than `tf.keras.Sequential()`. |

---

### **Building a Model Using the Functional API**  

#### **Step 1: Define the Input Layer**
```python
import tensorflow as tf

inputs = tf.keras.Input(shape=(100,))
```

#### **Step 2: Add Layers Using Functional Connections**
```python
x = tf.keras.layers.Dense(64, activation='relu')(inputs)
x = tf.keras.layers.Dense(32, activation='relu')(x)
outputs = tf.keras.layers.Dense(10, activation='softmax')(x)
```

#### **Step 3: Create the Model**
```python
model = tf.keras.Model(inputs=inputs, outputs=outputs)
```

---

### **Model Compilation**
```python
model.compile(optimizer='adam',
              loss='sparse_categorical_crossentropy',
              metrics=['accuracy'])
```

---

### **Training the Model**
```python
history = model.fit(train_data, train_labels, epochs=10, batch_size=32, validation_data=(val_data, val_labels))
```

---

### **Evaluating and Predicting**  
```python
loss, accuracy = model.evaluate(test_data, test_labels)
predictions = model.predict(new_data)
```

---

### **Advanced Use Cases**  

#### **Multiple Inputs and Outputs**
```python
input_a = tf.keras.Input(shape=(64,))
input_b = tf.keras.Input(shape=(32,))

x1 = tf.keras.layers.Dense(32, activation='relu')(input_a)
x2 = tf.keras.layers.Dense(16, activation='relu')(input_b)

merged = tf.keras.layers.concatenate([x1, x2])
output = tf.keras.layers.Dense(10, activation='softmax')(merged)

model = tf.keras.Model(inputs=[input_a, input_b], outputs=output)
```

#### **Skip Connections (ResNet-like Architecture)**
```python
inputs = tf.keras.Input(shape=(64,))
x = tf.keras.layers.Dense(32, activation='relu')(inputs)
skip = tf.keras.layers.Dense(32, activation='relu')(x)
x = tf.keras.layers.add([x, skip])  # Skip Connection
outputs = tf.keras.layers.Dense(10, activation='softmax')(x)

model = tf.keras.Model(inputs=inputs, outputs=outputs)
```

---

### **Key Differences: Functional API vs. Sequential API**  

| **Feature** | **Functional API** | **Sequential API** |
|------------|-------------------|-------------------|
| **Multiple Inputs/Outputs** | ✅ Supported | ❌ Not Supported |
| **Skip Connections** | ✅ Supported | ❌ Not Supported |
| **Layer Reuse** | ✅ Possible | ❌ Not Possible |
| **Graph-based Model** | ✅ Yes | ❌ No |
| **Ease of Use** | ❌ More complex | ✅ Simpler |

---

### **Conclusion**  
- **Use Functional API** when working with complex architectures.  
- It is **more flexible** and allows for **custom network structures**.  
- For simple models, **Sequential API is easier to implement**.