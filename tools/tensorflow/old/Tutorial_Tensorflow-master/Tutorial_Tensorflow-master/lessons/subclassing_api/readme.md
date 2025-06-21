## **Subclassing API in TensorFlow**  

### **Overview**  
The **Subclassing API** in TensorFlow provides the most flexible way to build **custom models** by subclassing `tf.keras.Model`. It allows full control over the **forward pass, layer creation, and computations**, making it ideal for **research and experimental architectures**.  

---

### **When to Use the Subclassing API?**  

| **Use Case** | **Description** |
|-------------|----------------|
| **Highly Custom Architectures** | Allows defining custom forward passes. |
| **Conditional Computations** | Supports dynamic computations (e.g., RNNs, attention mechanisms). |
| **Custom Layers** | Enables the creation of custom layers and blocks. |
| **Full Control** | Ideal for research and prototype models. |

---

### **Creating a Model Using the Subclassing API**  

#### **Step 1: Define a Custom Model Class**  
```python
import tensorflow as tf

class MyModel(tf.keras.Model):
    def __init__(self):
        super(MyModel, self).__init__()
        self.dense1 = tf.keras.layers.Dense(64, activation='relu')
        self.dense2 = tf.keras.layers.Dense(32, activation='relu')
        self.output_layer = tf.keras.layers.Dense(10, activation='softmax')

    def call(self, inputs):
        x = self.dense1(inputs)
        x = self.dense2(x)
        return self.output_layer(x)
```

#### **Step 2: Instantiate the Model**
```python
model = MyModel()
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

### **Creating a Model with Multiple Inputs and Outputs**  
```python
class MultiInputModel(tf.keras.Model):
    def __init__(self):
        super(MultiInputModel, self).__init__()
        self.dense1 = tf.keras.layers.Dense(32, activation='relu')
        self.dense2 = tf.keras.layers.Dense(16, activation='relu')
        self.output1 = tf.keras.layers.Dense(10, activation='softmax')
        self.output2 = tf.keras.layers.Dense(5, activation='sigmoid')

    def call(self, inputs):
        x1, x2 = inputs
        x1 = self.dense1(x1)
        x2 = self.dense2(x2)
        return self.output1(x1), self.output2(x2)

model = MultiInputModel()
```

---

### **Key Differences: Subclassing API vs. Functional API vs. Sequential API**  

| **Feature** | **Subclassing API** | **Functional API** | **Sequential API** |
|------------|--------------------|-------------------|-------------------|
| **Custom Forward Pass** | ✅ Yes | ❌ No | ❌ No |
| **Multiple Inputs/Outputs** | ✅ Supported | ✅ Supported | ❌ Not Supported |
| **Skip Connections** | ✅ Supported | ✅ Supported | ❌ Not Supported |
| **Ease of Use** | ❌ Most complex | ⚠️ Medium | ✅ Easiest |
| **Layer Reuse** | ✅ Yes | ✅ Yes | ❌ No |
| **Ideal for Research** | ✅ Best choice | ❌ Not ideal | ❌ Not ideal |

---

### **Conclusion**  
- **Use the Subclassing API** when you need **full control over model behavior**.  
- It is **best suited for dynamic, custom, and experimental architectures**.  
- For simpler models, **Functional API or Sequential API** is preferred.