## **KerasTuner in TensorFlow**  

### **Overview**  
KerasTuner is a **hyperparameter tuning framework** built on TensorFlow and Keras that automates the process of finding the best hyperparameters for deep learning models.

---

## **1. Why Use KerasTuner?**  

| **Feature** | **Description** |
|------------|----------------|
| **Automated Hyperparameter Tuning** | Finds optimal learning rate, layer size, activation functions, etc. |
| **Multiple Search Algorithms** | Supports **Random Search, Hyperband, and Bayesian Optimization**. |
| **Easy Integration with Keras** | Works with `tf.keras` models. |
| **Scalability** | Can run on CPU, GPU, and TPU. |
| **Logging & Tracking** | Saves tuning results for future analysis. |

---

## **2. Installation**  

```bash
pip install keras-tuner
```

---

## **3. Hyperparameter Search Algorithms**  

| **Search Method** | **Description** |
|------------------|----------------|
| **RandomSearch** | Randomly samples hyperparameters within the defined space. |
| **Hyperband** | Efficient search using adaptive resource allocation. |
| **BayesianOptimization** | Uses past results to predict better hyperparameter choices. |
| **GridSearch** *(unofficial)* | Searches all possible combinations (not included in KerasTuner). |

---

## **4. How to Use KerasTuner**  

### **A. Define the Model with Hyperparameters**  
```python
import keras_tuner as kt
import tensorflow as tf
from tensorflow import keras

# Define a function for hyperparameter tuning
def model_builder(hp):
    model = keras.Sequential()
    
    # Tune the number of units in the first dense layer
    hp_units = hp.Int('units', min_value=32, max_value=512, step=32)
    model.add(keras.layers.Dense(units=hp_units, activation='relu'))
    model.add(keras.layers.Dense(10, activation='softmax'))
    
    # Tune the learning rate
    hp_learning_rate = hp.Choice('learning_rate', values=[0.001, 0.01, 0.1])
    
    model.compile(optimizer=keras.optimizers.Adam(learning_rate=hp_learning_rate),
                  loss='sparse_categorical_crossentropy',
                  metrics=['accuracy'])
    return model
```

---

### **B. Select a Tuning Strategy**  
```python
tuner = kt.RandomSearch(
    model_builder,
    objective='val_accuracy',
    max_trials=5,  # Number of different models to try
    executions_per_trial=1,  # Number of times to train each model
    directory='my_tuning',
    project_name='hyperparameter_search'
)
```
- **max_trials**: Total number of different hyperparameter sets to try.
- **executions_per_trial**: Runs each model multiple times for stability.

---

### **C. Load Data & Start Tuning**  
```python
(x_train, y_train), (x_val, y_val) = keras.datasets.mnist.load_data()
x_train, x_val = x_train / 255.0, y_val / 255.0

# Start the tuning process
tuner.search(x_train, y_train, epochs=10, validation_data=(x_val, y_val))
```

---

### **D. Retrieve the Best Hyperparameters**  
```python
# Get the best model
best_hps = tuner.get_best_hyperparameters(num_trials=1)[0]

print(f"Best number of units: {best_hps.get('units')}")
print(f"Best learning rate: {best_hps.get('learning_rate')}")
```

---

## **5. Advanced Search Methods**  

### **A. Hyperband Search** (Efficient Search)  
```python
tuner = kt.Hyperband(
    model_builder,
    objective='val_accuracy',
    max_epochs=20,
    factor=3,
    directory='hyperband_tuning',
    project_name='hyperband'
)
```
- Uses early stopping to eliminate poor models quickly.

---

### **B. Bayesian Optimization** (Smart Search)  
```python
tuner = kt.BayesianOptimization(
    model_builder,
    objective='val_accuracy',
    max_trials=10,
    directory='bayesian_tuning',
    project_name='bayesian'
)
```
- Uses probability to find the best hyperparameters based on past results.

---

## **6. Summary**  

- **KerasTuner automates hyperparameter tuning** for deep learning models.  
- **Supports multiple tuning strategies**: Random Search, Hyperband, and Bayesian Optimization.  
- **Works with any Keras model**, making it easy to integrate into workflows.  
- **Saves tuning history**, allowing reuse of best models later.  
- **Scalable across different hardware**, including CPUs, GPUs, and TPUs.  