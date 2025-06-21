# Distributed Training

---

## What Is Distributed Training?

Distributed training in TensorFlow enables scaling model training across **multiple GPUs, CPUs, or TPUs**, either on a single machine or across multiple nodes, improving **speed**, **efficiency**, and **model size capability**.

TensorFlow uses the **`tf.distribute.Strategy`** API to handle distribution logic.

---

## Core Strategies

| Strategy                      | Use Case                                      | Hardware Scope         |
| ----------------------------- | --------------------------------------------- | ---------------------- |
| `MirroredStrategy`            | Single machine, multiple GPUs                 | Multi-GPU (1 machine)  |
| `MultiWorkerMirroredStrategy` | Multi-machine synchronous training            | Multi-GPU (multi-node) |
| `TPUStrategy`                 | TPU training (e.g., Google Colab, Cloud TPUs) | TPUs                   |
| `ParameterServerStrategy`     | Asynchronous training on large clusters       | Distributed, scale-out |
| `CentralStorageStrategy`      | CPU-based central storage for variables       | CPU-based experiments  |

---

## 1. `MirroredStrategy`

### Description:

Uses synchronous training with **data parallelism** across multiple GPUs on a single machine.

### Usage:

```python
strategy = tf.distribute.MirroredStrategy()

with strategy.scope():
    model = create_model()
    model.compile(...)
```

---

## 2. `MultiWorkerMirroredStrategy`

### Description:

Synchronous training across multiple machines (workers).

### Environment Setup:

```bash
TF_CONFIG='{
  "cluster": {
    "worker": ["host1:port", "host2:port"]
  },
  "task": {"type": "worker", "index": 0}
}'
```

### Usage:

```python
strategy = tf.distribute.MultiWorkerMirroredStrategy()
with strategy.scope():
    model = create_model()
    model.compile(...)
```

---

## 3. `TPUStrategy`

### Description:

Used to train models on **Cloud TPUs** for high-performance, large-scale training.

### Usage (Colab/Cloud TPU):

```python
resolver = tf.distribute.cluster_resolver.TPUClusterResolver()
tf.config.experimental_connect_to_cluster(resolver)
tf.tpu.experimental.initialize_tpu_system(resolver)
strategy = tf.distribute.TPUStrategy(resolver)

with strategy.scope():
    model = create_model()
    model.compile(...)
```

---

## 4. `ParameterServerStrategy` (Asynchronous)

### Description:

Scales training across hundreds of machines using **parameter servers** and **workers**.

* Each variable is placed on a server.
* Each worker computes and updates asynchronously.

### Use Case:

* Huge models and datasets
* Sparse data (e.g., recommendation systems)

---

## 5. `CentralStorageStrategy`

### Description:

Variables are stored on the **CPU**, and computations run on all devices.

### Use Case:

* Debugging or experiments where compute cost isn’t a bottleneck.

---

## Data Input with `tf.data`

To work efficiently with strategies:

```python
dataset = tf.data.Dataset.from_tensor_slices((x, y)).shuffle(1024).batch(32)
strategy.experimental_distribute_dataset(dataset)
```

For multi-worker training:

```python
tf.data.experimental.AutoShardPolicy.DATA
```

---

## Training Syntax

### Using `fit()` API

```python
with strategy.scope():
    model = build_model()
    model.compile(...)
    model.fit(train_dataset, ...)
```

### Custom Training Loop

You must use `strategy.run()`:

```python
@tf.function
def train_step(inputs):
    def step_fn(inputs):
        ...
    strategy.run(step_fn, args=(inputs,))
```

---

## Best Practices

* **Use `strategy.scope()`** when creating and compiling models.
* Scale `batch_size` linearly with the number of replicas.
* Use **`tf.data` pipelines** with `prefetch()`, `cache()` for performance.
* Monitor for **gradient accumulation or imbalance** on multi-GPU setups.

---

## Debugging & Profiling Tools

| Tool                            | Purpose                       |
| ------------------------------- | ----------------------------- |
| TensorBoard Profiler            | Visualize device utilization  |
| `tf.print` inside `tf.function` | Debug graphs                  |
| `strategy.num_replicas_in_sync` | Check number of replicas used |

---

## Summary Table

| Strategy                      | Multi-GPU | Multi-Node | Use Case                       |
| ----------------------------- | --------- | ---------- | ------------------------------ |
| `MirroredStrategy`            | ✅         | ❌          | Most local multi-GPU scenarios |
| `MultiWorkerMirroredStrategy` | ✅         | ✅          | Cloud, cluster training        |
| `TPUStrategy`                 | ❌         | ✅ (TPU)    | Cloud TPU acceleration         |
| `ParameterServerStrategy`     | ✅         | ✅          | Scalable asynchronous training |
| `CentralStorageStrategy`      | ✅ (slow)  | ❌          | Debugging, prototyping         |

---
