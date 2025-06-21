## **TensorFlow.js Training**  

### **Overview**  
TensorFlow.js allows training models in the browser or Node.js environment using the `tf.Model` API. Training can be performed on custom models created using the **Sequential API**, **Functional API**, or **Graph Model**.  

---

### **1. Defining a Model for Training**  
Models in TensorFlow.js can be created using the **Sequential API** or **Functional API**.  

#### **Example: Creating a Sequential Model**
```javascript
const model = tf.sequential({
    layers: [
        tf.layers.dense({units: 32, inputShape: [10], activation: 'relu'}),
        tf.layers.dense({units: 1, activation: 'sigmoid'})
    ]
});
```

---

### **2. Compiling the Model**  
Before training, a model must be compiled with:  
- **Loss function** – Measures model performance.  
- **Optimizer** – Adjusts model parameters to minimize loss.  
- **Metrics** – Evaluates performance during training.  

#### **Example: Model Compilation**
```javascript
model.compile({
    optimizer: 'adam',
    loss: 'binaryCrossentropy',
    metrics: ['accuracy']
});
```

---

### **3. Preparing Data for Training**  

Data can be provided as:  
- **JavaScript arrays**  
- **Tensors (`tf.tensor`)**  
- **TF.js `tf.data.Dataset` API**  

#### **Example: Creating Training Data**
```javascript
const xs = tf.tensor2d([[0], [1], [2], [3]], [4, 1]);
const ys = tf.tensor2d([[0], [1], [1], [0]], [4, 1]);
```

---

### **4. Training the Model**  

Training is performed using `model.fit()` or `model.fitDataset()`.  

#### **Example: Training with `model.fit()`**
```javascript
await model.fit(xs, ys, {
    epochs: 100,
    batchSize: 2,
    callbacks: {
        onEpochEnd: (epoch, logs) => console.log(`Epoch ${epoch}: Loss = ${logs.loss}`)
    }
});
```

#### **Example: Training with `tf.data.Dataset`**
```javascript
const dataset = tf.data.array([{xs: [0], ys: [0]}, {xs: [1], ys: [1]}])
    .batch(2);
await model.fitDataset(dataset, {
    epochs: 100
});
```

---

### **5. Evaluating the Model**  
After training, the model can be evaluated on test data.  

#### **Example: Model Evaluation**
```javascript
const testXs = tf.tensor2d([[1.5], [2.5]], [2, 1]);
const testYs = tf.tensor2d([[1], [0]], [2, 1]);
const evalResult = model.evaluate(testXs, testYs);
evalResult.print();
```

---

### **6. Making Predictions**  
The trained model can be used to predict new data.  

#### **Example: Model Prediction**
```javascript
const newInput = tf.tensor2d([[2]], [1, 1]);
const prediction = model.predict(newInput);
prediction.print();
```

---

### **7. Saving the Model**  
Trained models can be saved locally or in IndexedDB.  

#### **Example: Save Model to Local Storage**
```javascript
await model.save('localstorage://my-trained-model');
```

#### **Example: Save Model to IndexedDB**
```javascript
await model.save('indexeddb://my-trained-model');
```

#### **Example: Save Model to File**
```javascript
await model.save('downloads://my-model');
```

---

### **8. Loading a Trained Model**  
A saved model can be reloaded for inference or retraining.  

#### **Example: Load Model from Local Storage**
```javascript
const loadedModel = await tf.loadLayersModel('localstorage://my-trained-model');
```

---

### **9. Training in a Web Worker**  
To avoid freezing the UI, training can run in a Web Worker.  

#### **Example: Running Training in a Web Worker**
```javascript
const worker = new Worker('worker.js');
worker.postMessage({model: myModel.toJSON(), trainData: myData});
```

---

### **10. Summary**  

| **Task** | **Method** |
|---------|-----------|
| Create a model | `tf.sequential()`, `tf.model()` |
| Compile a model | `model.compile()` |
| Train with arrays | `model.fit(xs, ys, options)` |
| Train with dataset | `model.fitDataset(dataset, options)` |
| Evaluate model | `model.evaluate(xs, ys)` |
| Make predictions | `model.predict(xs)` |
| Save model | `model.save(url)` |
| Load model | `tf.loadLayersModel(url)` |

---

### **Conclusion**  
- TensorFlow.js supports **browser-based training** using Tensors and Datasets.  
- Training is performed using **`model.fit()`** or **`model.fitDataset()`**.  
- Models can be **saved and loaded** for reuse and deployment.  
- Training can be **offloaded to Web Workers** to improve performance.