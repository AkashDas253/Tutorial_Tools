# Quantization, Pruning, and Model Optimization

---

TensorFlow provides model optimization techniques that help reduce model size, improve inference speed, and make deployment efficient — especially for mobile and edge devices.

These techniques are available through the **TensorFlow Model Optimization Toolkit** (`tensorflow_model_optimization`).

---

## 🔧 Optimization Techniques Overview

| Technique                  | Goal                                     | When to Use                                  |
| -------------------------- | ---------------------------------------- | -------------------------------------------- |
| **Quantization**           | Reduce model size and speed up inference | For deployment (especially mobile/edge)      |
| **Pruning**                | Reduce computation by removing weights   | For sparse models without much accuracy drop |
| **Clustering**             | Group weights into clusters              | For hardware-efficient compression           |
| **Knowledge Distillation** | Train small models to mimic large models | For custom lightweight deployments           |

---

## 1. **Quantization**

### What It Does:

* Converts float32 weights/activations to **int8**, **float16**, or other smaller types.
* Reduces **model size**, **memory footprint**, and **latency**.

### Types of Quantization

| Type                                  | Description                           | When to Use                       |
| ------------------------------------- | ------------------------------------- | --------------------------------- |
| **Post-Training Quantization**        | Quantize after training               | Quick optimization for deployment |
| **Quantization-Aware Training (QAT)** | Simulate quantization during training | Higher accuracy preservation      |

---

### a) Post-Training Quantization Example

```python
converter = tf.lite.TFLiteConverter.from_saved_model("model_path")
converter.optimizations = [tf.lite.Optimize.DEFAULT]
tflite_quant_model = converter.convert()
```

* For full int8:

```python
converter.target_spec.supported_ops = [tf.lite.OpsSet.TFLITE_BUILTINS_INT8]
converter.inference_input_type = tf.int8
converter.inference_output_type = tf.int8
```

### b) Quantization-Aware Training (QAT)

```python
import tensorflow_model_optimization as tfmot

quantize_model = tfmot.quantization.keras.quantize_model
q_model = quantize_model(model)

q_model.compile(optimizer, loss, metrics)
q_model.fit(train_data, epochs=5)
```

---

## 2. **Pruning**

### What It Does:

* Removes unimportant weights (sets them to 0) during training.
* Produces sparse models with fewer computations.

### Use Cases:

* Reduce model size while maintaining accuracy.
* Prepare for sparse inference backends.

### How to Apply:

```python
import tensorflow_model_optimization as tfmot

prune_low_magnitude = tfmot.sparsity.keras.prune_low_magnitude

pruning_params = {
    "pruning_schedule": tfmot.sparsity.keras.PolynomialDecay(
        initial_sparsity=0.0,
        final_sparsity=0.5,
        begin_step=0,
        end_step=end_step
    )
}

model_for_pruning = prune_low_magnitude(model, **pruning_params)

model_for_pruning.compile(...)
model_for_pruning.fit(train_data, callbacks=[tfmot.sparsity.keras.UpdatePruningStep()])
```

### Strip Pruning for Export:

```python
model_stripped = tfmot.sparsity.keras.strip_pruning(model_for_pruning)
model_stripped.save('pruned_model.h5')
```

---

## 3. **Weight Clustering**

### What It Does:

* Constrains weight values into a fixed number of clusters.
* Makes models more compressible and hardware efficient.

### Example:

```python
clustering_params = {
  'number_of_clusters': 16,
  'cluster_centroids_init': 'linear'
}

clustered_model = tfmot.clustering.keras.cluster_weights(model, **clustering_params)
clustered_model.compile(...)
clustered_model.fit(...)
```

---

## 4. **Knowledge Distillation**

### What It Does:

* A **small "student" model** is trained to mimic a **large "teacher" model**.
* Balances performance and efficiency.

### Key Steps:

* Train or load a large, accurate model.
* Create a smaller model.
* Train it using a loss that includes both:

  * Ground truth labels
  * Teacher predictions

> TensorFlow doesn’t have native support for distillation, but it's easy to implement using custom training loops.

---

## 5. **Combining Optimization Techniques**

* **QAT + Pruning**: Prune first → Fine-tune with quantization-aware training.
* **Pruning + Clustering**: Reduces size even more.
* **QAT + Post-training int8 Export**: For highest deployment compatibility.

---

## Optimization Summary Table

| Technique                  | Size ↓ | Speed ↑          | Accuracy ↔     | Training Needed | Use Case                      |
| -------------------------- | ------ | ---------------- | -------------- | --------------- | ----------------------------- |
| Post-Training Quantization | ✅      | ✅                | Minor drop     | ❌               | Fast deploy to mobile         |
| QAT                        | ✅      | ✅                | Best preserved | ✅               | Critical accuracy apps        |
| Pruning                    | ✅      | ✅ (if supported) | Slight drop    | ✅               | Reduce FLOPs/size             |
| Clustering                 | ✅      | ❌                | Slight drop    | ✅               | Compressibility               |
| Distillation               | ✅      | ✅                | Maintains      | ✅               | Student models for deployment |

---

## Deployment Targets

| Platform             | Preferred Format    | Recommended Optimization   |
| -------------------- | ------------------- | -------------------------- |
| Mobile (Android/iOS) | `TFLite`            | Post-training quantization |
| Edge IoT             | `TFLite Micro`      | Pruned + Quantized         |
| Web (TF.js)          | `TF.js Graph Model` | Weight compression         |
| Server               | `SavedModel`        | Can benefit from pruning   |

---

## Monitoring & Evaluation

* Evaluate optimized models using `evaluate()` or `TFLiteInterpreter`.
* Use `TensorBoard` to track pruning and sparsity during training.
* Profile latency and size using:

  * `TFLite Interpreter`
  * `tf.lite.experimental.Analyzer`
  * `Netron` (for model structure)

---
