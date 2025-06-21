# Model Deployment

---

## What Is Model Deployment?

Model deployment is the process of **exporting**, **serving**, and **integrating** a trained model into a **production environment** where it can make predictions on real-world data.

---

## Key Steps in Deployment

| Stage              | Description                                  |
| ------------------ | -------------------------------------------- |
| Model Exporting    | Save trained model in a portable format      |
| Serving            | Make model accessible via APIs or services   |
| Client Integration | Use the model in applications or pipelines   |
| Monitoring         | Track model health and usage post-deployment |

---

## 1. Model Export Formats

| Format                 | Description                                                |
| ---------------------- | ---------------------------------------------------------- |
| `SavedModel` (default) | Directory with model architecture, weights, and signatures |
| `HDF5 (.h5)`           | Older single-file format (Keras-compatible)                |
| `TFLite`               | Optimized for edge/mobile devices                          |
| `TF.js`                | For running in web browsers                                |
| `ONNX`                 | Interoperable format for other platforms                   |

### Saving Example

```python
model.save('path/to/saved_model')          # SavedModel format
model.save('model.h5')                     # HDF5 format
```

---

## 2. Serving with TensorFlow Serving

**TensorFlow Serving** is a flexible, high-performance server for serving ML models in production environments.

### Export Directory Structure

```
/models/
  /my_model/
    /1/
      saved_model.pb
      variables/
```

### Docker Setup

```bash
docker run -p 8501:8501 \
 --mount type=bind,source=$(pwd)/models/my_model,target=/models/my_model \
 -e MODEL_NAME=my_model -t tensorflow/serving
```

### REST API Example

```bash
curl -X POST http://localhost:8501/v1/models/my_model:predict \
  -d '{"instances": [[1.0, 2.0, 3.0, 4.0]]}'
```

---

## 3. TensorFlow Lite (TFLite) – Edge/Mobile

### Convert to TFLite

```python
converter = tf.lite.TFLiteConverter.from_saved_model('path/to/model')
tflite_model = converter.convert()

with open('model.tflite', 'wb') as f:
    f.write(tflite_model)
```

### Use in Mobile (e.g., Android)

* Add TFLite model to assets
* Use TensorFlow Lite Interpreter in app code

---

## 4. TensorFlow\.js – Browser

### Convert to TF.js

```bash
tensorflowjs_converter \
  --input_format=tf_saved_model \
  path/to/saved_model path/to/tfjs_model
```

### Use in Web App

```javascript
const model = await tf.loadLayersModel('model/model.json');
```

---

## 5. ONNX – Interoperability

Convert TensorFlow model to ONNX using:

```bash
pip install tf2onnx
python -m tf2onnx.convert --saved-model path/to/saved_model --output model.onnx
```

---

## 6. Deployment Options

| Method         | Environment         | Tools                              |
| -------------- | ------------------- | ---------------------------------- |
| REST API       | Backend server      | TensorFlow Serving, Flask, FastAPI |
| gRPC API       | Cloud/microservices | TensorFlow Serving                 |
| Web App        | Browser             | TensorFlow\.js                     |
| Mobile         | Android, iOS        | TensorFlow Lite                    |
| Embedded/IoT   | Edge devices        | TFLite Micro                       |
| Cross-platform | Multi-framework     | ONNX                               |

---

## 7. Cloud Deployment

| Platform                     | Method                             |
| ---------------------------- | ---------------------------------- |
| **Google Cloud AI Platform** | Deploy SavedModel directly         |
| **AWS SageMaker**            | Convert to container or ONNX model |
| **Azure ML**                 | Custom container or ONNX           |

---

## 8. Model Versioning and A/B Testing

* Use versioned folders (`/models/model_name/1/`, `/2/`)
* Serve multiple versions concurrently via TensorFlow Serving
* Load-balancing for traffic splitting during rollout

---

## 9. Monitoring and Logging

* Monitor latency, throughput, accuracy drift
* Use Prometheus, Grafana, or cloud-native tools
* Enable custom logging in `tf.keras.callbacks.Callback`

---

## 10. Security and Optimization

| Strategy              | Purpose                                |
| --------------------- | -------------------------------------- |
| Quantization (TFLite) | Reduce model size                      |
| Pruning               | Remove unused weights                  |
| Encrypted Serving     | Secure API communication (HTTPS, Auth) |
| Signature Definition  | Define exact input/output schema       |

---

## Summary Table

| Target         | Format     | Deployment Tool                |
| -------------- | ---------- | ------------------------------ |
| Server/Backend | SavedModel | TensorFlow Serving, Flask      |
| Mobile/Edge    | TFLite     | TensorFlow Lite                |
| Web            | TF.js      | TensorFlow\.js                 |
| Cross-platform | ONNX       | ONNX runtime                   |
| Cloud          | SavedModel | GCP AI Platform, AWS SageMaker |

---
