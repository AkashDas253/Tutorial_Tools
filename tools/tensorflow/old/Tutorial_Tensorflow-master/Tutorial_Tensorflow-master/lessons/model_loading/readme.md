## **Model Loading in TensorFlow**  

### **Overview**  
Model loading is essential for resuming training, making predictions, or deploying a trained model. TensorFlow provides different ways to load a saved model based on the format used for saving.  

---

### **1. Loading a Model in SavedModel Format**  

#### **Loading the Entire Model**  
```python
loaded_model = tf.keras.models.load_model("saved_model_directory")
```
- Loads architecture, weights, and optimizer state.  
- Works with models saved using `model.save("saved_model_directory")`.  

#### **Making Predictions with the Loaded Model**  
```python
predictions = loaded_model.predict(test_data)
```

---

### **2. Loading a Model in HDF5 Format**  

#### **Loading the Model**  
```python
loaded_model = tf.keras.models.load_model("model.h5")
```
- Works with models saved using `model.save("model.h5")`.  

---

### **3. Loading Model Weights Only**  

#### **Loading Weights into an Identical Model**  
```python
model.load_weights("weights_checkpoint")
```
- The model must have the same architecture as the original model.  

#### **Loading Checkpoint Weights**  
```python
model.load_weights("checkpoints/cp.ckpt")
```
- Useful when training with checkpoints.  

---

### **4. Loading the Best Model from Checkpoints**  

```python
best_model = tf.keras.models.load_model("best_model.h5")
```
- Restores the best-performing model saved during training.  

---

### **5. Loading a Custom Model (Subclassing API)**  

#### **Defining the Model and Loading Weights**  
```python
class CustomModel(tf.keras.Model):
    def __init__(self):
        super(CustomModel, self).__init__()
        self.dense = tf.keras.layers.Dense(10)

    def call(self, inputs):
        return self.dense(inputs)

model = CustomModel()
model.build(input_shape=(None, 5))  # Ensure model structure is defined
model.load_weights("custom_model_weights")
```
- Requires manually defining the model before loading weights.  

---

### **6. Loading a Model with Custom Objects**  

#### **Saving with a Custom Loss Function or Layer**  
```python
def custom_loss(y_true, y_pred):
    return tf.reduce_mean(tf.square(y_true - y_pred))

model.compile(optimizer="adam", loss=custom_loss)
model.save("custom_model.h5")
```

#### **Loading with Custom Objects**  
```python
loaded_model = tf.keras.models.load_model("custom_model.h5", custom_objects={"custom_loss": custom_loss})
```
- Ensures compatibility with non-standard components.  

---

### **7. Loading a Model Saved as a TensorFlow Hub Module**  

```python
import tensorflow_hub as hub

hub_model = tf.keras.models.load_model("hub_model", custom_objects={"KerasLayer": hub.KerasLayer})
```
- Used when loading models from **TensorFlow Hub**.  

---

### **Conclusion**  
- **SavedModel**: Use `tf.keras.models.load_model("path")` for TensorFlow deployment.  
- **HDF5**: Load `.h5` files for Keras compatibility.  
- **Weights Only**: Load using `.load_weights("path")` if architecture remains unchanged.  
- **Custom Objects**: Specify `custom_objects={}` when loading custom layers or losses.  
- **Checkpoint-Based Loading**: Useful for resuming training or selecting the best model.