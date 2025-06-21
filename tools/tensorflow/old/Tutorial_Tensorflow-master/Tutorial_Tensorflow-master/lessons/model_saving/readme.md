## **Model Saving in TensorFlow**  

### **Overview**  
Saving a trained model is essential for deployment, sharing, or resuming training. TensorFlow provides two main ways to save models:  

| **Method** | **Description** |
|-----------|----------------|
| **SavedModel format** (`.pb`) | Recommended format for TensorFlow deployment, supports Python & other languages. |
| **HDF5 format** (`.h5`) | Compatible with Keras, useful for small models & portability. |

---

### **1. Saving and Loading a Model in SavedModel Format**  

#### **Saving the Model**  
```python
model.save("saved_model_directory")
```
- Saves architecture, weights, training configuration, and optimizer state.  

#### **Loading the Model**  
```python
loaded_model = tf.keras.models.load_model("saved_model_directory")
```
- Restores the entire model with weights and optimizer state.  

---

### **2. Saving and Loading a Model in HDF5 Format**  

#### **Saving the Model**  
```python
model.save("model.h5")
```
- Saves everything in a single `.h5` file.  

#### **Loading the Model**  
```python
loaded_model = tf.keras.models.load_model("model.h5")
```
- Loads the entire model from the `.h5` file.  

---

### **3. Saving and Loading Only Model Weights**  

#### **Saving Weights**  
```python
model.save_weights("weights_checkpoint")
```

#### **Loading Weights**  
```python
model.load_weights("weights_checkpoint")
```
- Requires the same model architecture to restore weights properly.  

---

### **4. Saving and Loading Model Weights with Checkpoints**  

#### **Saving During Training**  
```python
checkpoint_path = "checkpoints/cp.ckpt"
checkpoint_callback = tf.keras.callbacks.ModelCheckpoint(filepath=checkpoint_path, save_weights_only=True, verbose=1)

model.fit(train_dataset, epochs=10, callbacks=[checkpoint_callback])
```
- Saves model weights after each epoch.  

#### **Loading from Checkpoint**  
```python
model.load_weights("checkpoints/cp.ckpt")
```
- Restores model weights before continuing training.  

---

### **5. Auto-Saving Best Model with Checkpoints**  

```python
checkpoint_path = "best_model.h5"
checkpoint_callback = tf.keras.callbacks.ModelCheckpoint(filepath=checkpoint_path, save_best_only=True, monitor="val_loss", verbose=1)

model.fit(train_dataset, epochs=10, validation_data=val_dataset, callbacks=[checkpoint_callback])
```
- Saves only the best model based on `val_loss`.  

---

### **6. Saving a Model as a TensorFlow Hub Module (For Reuse & Deployment)**  

#### **Saving the Model**  
```python
import tensorflow_hub as hub
hub_model_path = "hub_model"
model.save(hub_model_path, include_optimizer=False)
```

#### **Loading the Model**  
```python
hub_model = tf.keras.models.load_model(hub_model_path, custom_objects={"KerasLayer": hub.KerasLayer})
```
- Useful for TensorFlow Hub deployments.  

---

### **7. Saving a Custom Model (Subclassing API)**  

#### **Saving Weights Only**  
```python
class CustomModel(tf.keras.Model):
    def __init__(self):
        super(CustomModel, self).__init__()
        self.dense = tf.keras.layers.Dense(10)

    def call(self, inputs):
        return self.dense(inputs)

model = CustomModel()
model.build(input_shape=(None, 5))
model.save_weights("custom_model_weights")
```

#### **Restoring Weights**  
```python
new_model = CustomModel()
new_model.build(input_shape=(None, 5))
new_model.load_weights("custom_model_weights")
```
- This method only saves and restores model weights, not architecture.  

---

### **Conclusion**  
- Use **SavedModel** for deployment.  
- Use **HDF5 format** for compatibility with Keras.  
- Save **only weights** when architecture is predefined.  
- Use **checkpoints** to save models during training.  
- **Best model saving** ensures optimal performance.