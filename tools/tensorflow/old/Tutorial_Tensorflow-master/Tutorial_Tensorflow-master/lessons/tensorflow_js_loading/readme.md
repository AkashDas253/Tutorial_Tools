## **TensorFlow.js Model Loading**  

### **Overview**  
TensorFlow.js allows loading and running pre-trained models in a web browser or Node.js environment. Models can be loaded from different sources, including URLs, local files, IndexedDB, or user-uploaded files.  

---

### **1. Methods to Load Models**  

| **Method** | **Description** |
|------------|---------------|
| `tf.loadLayersModel(url)` | Loads a Keras-based model (Sequential/Functional API) from a given URL or file. |
| `tf.loadGraphModel(url)` | Loads a TensorFlow SavedModel or frozen graph for inference. |
| `tf.models.modelFromJSON(json)` | Loads a model from a JSON file (for Keras models). |

---

### **2. Loading a Model from a URL**  
Pre-trained models can be hosted on a server and loaded in TensorFlow.js.  

#### **Example: Load a Keras Model (Layers Model)**
```javascript
const model = await tf.loadLayersModel('https://example.com/model.json');
```

#### **Example: Load a TensorFlow SavedModel (Graph Model)**
```javascript
const model = await tf.loadGraphModel('https://example.com/model/model.json');
```

---

### **3. Loading a Model from Local Files**  
Useful when models are stored locally in a web app or Node.js.  

#### **Example: Load a Local Model in Browser**
```javascript
const model = await tf.loadLayersModel('localstorage://my-model');
```

#### **Example: Load a Model from IndexedDB**
```javascript
const model = await tf.loadLayersModel('indexeddb://my-model');
```

---

### **4. Loading a Model from User Upload (Browser)**  
Users can upload their own `.json` and `.bin` files.  

```javascript
async function loadModelFromFile(event) {
    const files = event.target.files;
    const model = await tf.loadLayersModel(tf.io.browserFiles(files));
}
document.getElementById('upload').addEventListener('change', loadModelFromFile);
```

HTML:
```html
<input type="file" id="upload" multiple>
```

---

### **5. Model Storage Locations**  

| **Storage** | **Example URL** |
|-------------|----------------|
| **Remote URL** | `'https://example.com/model.json'` |
| **Local File (Browser)** | `'localstorage://my-model'` |
| **IndexedDB** | `'indexeddb://my-model'` |
| **File Upload** | `tf.io.browserFiles(files)` |

---

### **6. Checking Model Layers & Summary**  
Once a model is loaded, it can be inspected.  

```javascript
console.log(model.summary());
console.log(model.layers);
```

---

### **7. Running Inference on a Loaded Model**  
After loading a model, input tensors can be passed for predictions.  

```javascript
const input = tf.tensor([1, 2, 3, 4]);  // Example input
const output = model.predict(input);
output.print();
```

---

### **8. Converting TensorFlow/Keras Models to TensorFlow.js Format**  

To load models in TensorFlow.js, they must be converted using the **TensorFlow.js Converter**.

#### **Installation**
```sh
pip install tensorflowjs
```

#### **Convert a Keras Model to TensorFlow.js**
```sh
tensorflowjs_converter --input_format keras model.h5 web_model/
```

#### **Convert a SavedModel to TensorFlow.js**
```sh
tensorflowjs_converter --input_format=tf_saved_model --output_node_names='output' saved_model web_model/
```

---

### **9. Summary**  

| **Task** | **Method** |
|---------|-----------|
| Load a Keras model | `tf.loadLayersModel(url)` |
| Load a TensorFlow model | `tf.loadGraphModel(url)` |
| Load from user upload | `tf.io.browserFiles(files)` |
| Load from IndexedDB | `'indexeddb://model-name'` |
| Run inference | `model.predict(input)` |

---

### **Conclusion**  
- TensorFlow.js supports **multiple model formats** (Keras, SavedModel, GraphDef).  
- Models can be loaded from **URLs, local storage, IndexedDB, and file uploads**.  
- After loading, models can be used for **inference, evaluation, and retraining**.