## **TensorFlow Serving**  

### **Overview**  
TensorFlow Serving is a system designed for serving machine learning models in production. It provides a flexible, high-performance way to deploy and manage ML models for real-time predictions via REST or gRPC APIs.  

---

### **1. Key Features**  

| **Feature** | **Description** |
|------------|----------------|
| **Efficient Model Management** | Supports loading, updating, and serving multiple versions of a model. |
| **High Performance** | Optimized for low-latency, high-throughput inference. |
| **Supports Multiple Models** | Can serve multiple models simultaneously. |
| **REST & gRPC APIs** | Provides easy access for web and mobile applications. |
| **Batch Processing** | Supports batch inference to improve performance. |

---

### **2. Installing TensorFlow Serving**  

#### **On Ubuntu (Recommended)**  
```bash
echo "deb [arch=amd64] https://storage.googleapis.com/tensorflow-serving-apt stable tensorflow-model-server main" | sudo tee /etc/apt/sources.list.d/tensorflow-serving.list
curl https://storage.googleapis.com/tensorflow-serving-apt/tensorflow-serving.release.pub.gpg | sudo apt-key add -
sudo apt update
sudo apt install tensorflow-model-server
```

#### **Using Docker**  
```bash
docker pull tensorflow/serving
```

---

### **3. Preparing a Model for TensorFlow Serving**  

#### **Saving the Model in `SavedModel` Format**  
```python
model.save("saved_model_directory")
```
- The directory must follow TensorFlow Serving's structure:  
```
saved_model_directory/
  ├── 1/
  │   ├── assets/
  │   ├── saved_model.pb
  │   ├── variables/
```
- `1/` represents the version number of the model.  

---

### **4. Running TensorFlow Serving**  

#### **Using TensorFlow Model Server**  
```bash
tensorflow_model_server --rest_api_port=8501 --model_name=my_model --model_base_path="$(pwd)/saved_model_directory" &
```
- Runs the server on port **8501** with the model name `my_model`.  

#### **Using Docker**  
```bash
docker run -p 8501:8501 --name=tf_serving --mount type=bind,source=$(pwd)/saved_model_directory,target=/models/my_model -e MODEL_NAME=my_model -t tensorflow/serving
```

---

### **5. Making Predictions via TensorFlow Serving**  

#### **Using REST API (JSON Input)**  
```bash
curl -d '{"signature_name":"serving_default","instances":[[1.0, 2.0, 3.0, 4.0]]}' -H "Content-Type: application/json" -X POST http://localhost:8501/v1/models/my_model:predict
```

#### **Using Python Requests Library**  
```python
import requests
import json

data = json.dumps({"signature_name": "serving_default", "instances": [[1.0, 2.0, 3.0, 4.0]]})
headers = {"content-type": "application/json"}
response = requests.post("http://localhost:8501/v1/models/my_model:predict", data=data, headers=headers)

print(response.json())
```

#### **Using gRPC API**  
```python
import tensorflow as tf
import grpc
from tensorflow_serving.apis import predict_pb2, prediction_service_pb2_grpc

channel = grpc.insecure_channel("localhost:8500")
stub = prediction_service_pb2_grpc.PredictionServiceStub(channel)

request = predict_pb2.PredictRequest()
request.model_spec.name = "my_model"
request.inputs["input_tensor"].CopyFrom(tf.make_tensor_proto([[1.0, 2.0, 3.0, 4.0]]))

result = stub.Predict(request, timeout=10)
print(result)
```

---

### **6. Managing Model Versions**  

#### **Updating a Model**  
- Place the new version inside `saved_model_directory/` (e.g., `saved_model_directory/2/`).  
- Restart TensorFlow Serving.  
- The server automatically loads the latest version.  

#### **Checking Available Versions**  
```bash
curl http://localhost:8501/v1/models/my_model/versions
```

---

### **7. Serving Multiple Models**  

#### **Serving Multiple Models at Once**  
```bash
tensorflow_model_server --rest_api_port=8501 --model_config_file=models.config &
```

#### **Example `models.config` File**  
```
model_config_list {
  config {
    name: "model1"
    base_path: "/models/model1"
    model_platform: "tensorflow"
  }
  config {
    name: "model2"
    base_path: "/models/model2"
    model_platform: "tensorflow"
  }
}
```

---

### **Conclusion**  
- **TensorFlow Serving** enables high-performance model deployment.  
- Supports **REST & gRPC APIs** for flexible integration.  
- **Docker and TensorFlow Model Server** provide easy deployment options.  
- Supports **model versioning and multiple models** in production.