# TensorFlow Concepts and Subconcepts  

## **1. Core TensorFlow**  
- **Tensors**  
  - Tensor structure  
  - Rank, shape, and dtype  
  - Broadcasting  
  - Operations on tensors  
- **Variables**  
  - Creating and assigning variables  
  - Variable scopes  
  - Trainable variables  
- **Operations**  
  - Math operations  
  - Logical operations  
  - Custom operations  

## **2. Computational Graphs and Execution**  
- **Eager Execution**  
  - Immediate operations  
  - Debugging with eager execution  
- **Graph Execution**  
  - Defining computation graphs  
  - `tf.function` and AutoGraph  
  - Graph optimizations  

## **3. Data Handling and Input Pipelines**  
- **TensorFlow Datasets (TFDS)**  
  - Loading datasets  
  - Preprocessing data  
- **`tf.data` API**  
  - Creating datasets  
  - Data transformations (`map`, `filter`, `batch`)  
  - Performance optimizations (`prefetch`, `shuffle`, `cache`)  
- **TFRecord Format**  
  - Writing and reading TFRecords  
  - Optimizing storage with TFRecords  

## **4. TensorFlow Models**  
- **Sequential API (`tf.keras.Sequential`)**  
  - Defining layers  
  - Configuring activation functions  
- **Functional API (`tf.keras.Model`)**  
  - Multi-input and multi-output models  
  - Custom model architectures  
- **Subclassing API**  
  - Custom layers  
  - Custom forward passes  

## **5. Layers and Activation Functions**  
- **Core Layers**  
  - Dense, Dropout, Flatten  
- **Convolutional Layers**  
  - Conv1D, Conv2D, Conv3D  
  - MaxPooling, AveragePooling  
- **Recurrent Layers**  
  - LSTM, GRU, SimpleRNN  
- **Normalization Layers**  
  - Batch Normalization  
  - Layer Normalization  
- **Activation Functions**  
  - ReLU, Sigmoid, Tanh, Softmax, Leaky ReLU  

## **6. Model Training and Evaluation**  
- **Loss Functions**  
  - Mean Squared Error, Cross-Entropy, Huber Loss  
- **Optimizers**  
  - SGD, Adam, RMSProp, Adagrad  
- **Metrics**  
  - Accuracy, Precision, Recall, AUC  
- **Model Compilation**  
  - Defining loss, optimizer, and metrics  
- **Training Process (`fit`)**  
  - Mini-batch training  
  - Using callbacks  
- **Custom Training Loops**  
  - `GradientTape`  
  - Manual backpropagation  

## **7. Model Saving and Deployment**  
- **Saving Models**  
  - `SavedModel` format  
  - HDF5 (`.h5`) format  
- **Loading Models**  
  - Restoring weights  
  - Transfer learning  
- **TensorFlow Serving**  
  - Model deployment pipeline  
  - gRPC and REST API deployment  

## **8. TensorFlow Lite (TFLite)**  
- **Model Conversion**  
  - Converting models to TFLite  
- **Optimizations**  
  - Quantization  
  - Pruning and clustering  
- **Deployment**  
  - Running models on mobile and edge devices  

## **9. TensorFlow.js**  
- **Model Loading and Execution in Browser**  
  - Running pre-trained models  
- **Building and Training Models in JavaScript**  
  - Tensor operations in JavaScript  
  - Training in the browser  

## **10. Distributed Training**  
- **Strategies for Distribution**  
  - `MirroredStrategy` (multi-GPU training)  
  - `TPUStrategy`  
  - `MultiWorkerMirroredStrategy`  
- **Model Parallelism vs Data Parallelism**  
- **Training on Cloud TPUs**  

## **11. TensorFlow Extended (TFX)**  
- **Pipeline Components**  
  - Data validation  
  - Model training  
  - Model deployment  
- **TensorFlow Data Validation (TFDV)**  
- **TensorFlow Model Analysis (TFMA)**  

## **12. AutoML with TensorFlow**  
- **AutoKeras**  
- **KerasTuner**  
- **Hyperparameter Optimization**  

## **13. Reinforcement Learning in TensorFlow**  
- **TF-Agents**  
  - Policy gradients  
  - Deep Q-Learning  
- **Integration with Gym Environments**  

## **14. Generative Models**  
- **GANs (Generative Adversarial Networks)**  
- **VAEs (Variational Autoencoders)**  

## **15. Time Series and Sequence Modeling**  
- **LSTMs and GRUs**  
- **Transformers and Self-Attention**  
- **Seq2Seq Models**  

## **16. Custom Operations and Extensions**  
- **Creating Custom Layers**  
- **Custom Training and Loss Functions**  
- **Extending TensorFlow with C++ Kernels**  
