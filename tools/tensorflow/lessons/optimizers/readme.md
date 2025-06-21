# Optimizers (`tf.keras.optimizers`)

---

## What Are Optimizers?

Optimizers adjust a model's **trainable parameters (weights)** to minimize the **loss function** by computing and applying **gradients** using **gradient descent** or its variants.

---

## Key Functions of an Optimizer

* Calculate gradients of the loss w\.r.t. model weights.
* Apply gradients to update the weights.
* Adjust learning rate or other internal parameters.

---

## Common Arguments for All Optimizers

| Argument          | Description                               | Default       |
| ----------------- | ----------------------------------------- | ------------- |
| `learning_rate`   | Step size for weight updates              | `0.001`       |
| `name`            | Name of the optimizer instance            | Auto-assigned |
| `clipnorm`        | Gradient clipping by norm                 | `None`        |
| `clipvalue`       | Gradient clipping by value                | `None`        |
| `global_clipnorm` | Clip global norm across all variables     | `None`        |
| `use_ema`         | Use exponential moving average of weights | `False`       |

---

## Built-in Optimizers

### 1. **SGD (Stochastic Gradient Descent)**

* Basic optimizer with optional momentum and Nesterov acceleration.

```python
tf.keras.optimizers.SGD(learning_rate=0.01, momentum=0.0, nesterov=False)
```

### 2. **Adam (Adaptive Moment Estimation)**

* Combines RMSprop and momentum; most commonly used.

```python
tf.keras.optimizers.Adam(
    learning_rate=0.001, beta_1=0.9, beta_2=0.999, epsilon=1e-7
)
```

### 3. **RMSprop**

* Maintains moving average of squared gradients; suitable for RNNs.

```python
tf.keras.optimizers.RMSprop(
    learning_rate=0.001, rho=0.9, momentum=0.0, epsilon=1e-7
)
```

### 4. **Adagrad**

* Adapts learning rate based on parameter updates; suitable for sparse data.

```python
tf.keras.optimizers.Adagrad(learning_rate=0.01, initial_accumulator_value=0.1)
```

### 5. **Adadelta**

* Improvement over Adagrad without a manually tuned learning rate.

```python
tf.keras.optimizers.Adadelta(learning_rate=1.0, rho=0.95, epsilon=1e-7)
```

### 6. **Adamax**

* Variant of Adam using the infinity norm.

```python
tf.keras.optimizers.Adamax(learning_rate=0.002, beta_1=0.9, beta_2=0.999)
```

### 7. **Nadam (Nesterov + Adam)**

* Combines Nesterov momentum with Adam.

```python
tf.keras.optimizers.Nadam(learning_rate=0.001, beta_1=0.9, beta_2=0.999)
```

### 8. **Ftrl (Follow The Regularized Leader)**

* Linear model optimizer for large-scale problems with L1/L2 regularization.

```python
tf.keras.optimizers.Ftrl(
    learning_rate=0.001, l1_regularization_strength=0.0, l2_regularization_strength=0.0
)
```

---

## Choosing the Right Optimizer

| Use Case                            | Recommended Optimizer  |
| ----------------------------------- | ---------------------- |
| Most general-purpose tasks          | `Adam`                 |
| Image classification                | `Adam`, `SGD+momentum` |
| Recurrent networks (e.g., RNNs)     | `RMSprop`, `Adam`      |
| Sparse data (e.g., NLP, embeddings) | `Adagrad`              |
| Budgeted tasks (low memory)         | `SGD`, `Adadelta`      |
| Large-scale linear models           | `Ftrl`                 |

---

## Learning Rate Schedules (Optional)

All optimizers accept a `learning_rate` which can also be a **schedule**:

```python
from tensorflow.keras.optimizers.schedules import ExponentialDecay

lr_schedule = ExponentialDecay(
    initial_learning_rate=0.01,
    decay_steps=10000,
    decay_rate=0.96
)

optimizer = tf.keras.optimizers.Adam(learning_rate=lr_schedule)
```

Other Schedules:

* `PiecewiseConstantDecay`
* `PolynomialDecay`
* `InverseTimeDecay`
* `CosineDecay`
* `CosineDecayRestarts`

---

## Gradient Clipping

To prevent exploding gradients:

```python
optimizer = tf.keras.optimizers.Adam(
    learning_rate=0.001,
    clipnorm=1.0
)
```

---

## Using Optimizers in Custom Training Loop

```python
with tf.GradientTape() as tape:
    predictions = model(x, training=True)
    loss = loss_fn(y, predictions)
grads = tape.gradient(loss, model.trainable_variables)
optimizer.apply_gradients(zip(grads, model.trainable_variables))
```

---

## Summary Table

| Optimizer  | Adaptive | Momentum | Use Case                                 |
| ---------- | -------- | -------- | ---------------------------------------- |
| `SGD`      | ❌        | ✅        | Simple models, baseline, experimentation |
| `Adam`     | ✅        | ✅        | General use, works well in most cases    |
| `RMSprop`  | ✅        | ✅        | RNNs, fast convergence                   |
| `Adagrad`  | ✅        | ❌        | Sparse data, NLP                         |
| `Adadelta` | ✅        | ❌        | Stable LR without tuning                 |
| `Adamax`   | ✅        | ✅        | Variant of Adam (more stable)            |
| `Nadam`    | ✅        | ✅        | Combines Adam with Nesterov momentum     |
| `Ftrl`     | ✅        | ❌        | Large-scale sparse linear models         |

---
