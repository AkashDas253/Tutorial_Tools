# Layers API (`tf.keras.layers`)

---

## What Is the Layers API?

`tf.keras.layers` provides modular, reusable building blocks for constructing neural networks in TensorFlow.
Each layer takes tensors as input, performs computation, and outputs tensors.

---

## Categories of Layers

### 1. Core Layers

| Layer          | Description                                  |
| -------------- | -------------------------------------------- |
| `Dense`        | Fully connected layer                        |
| `Activation`   | Applies activation function                  |
| `Dropout`      | Randomly sets inputs to 0 for regularization |
| `Flatten`      | Flattens input tensor                        |
| `Reshape`      | Reshapes tensor to desired shape             |
| `RepeatVector` | Repeats input for sequence modeling          |
| `Permute`      | Rearranges dimensions                        |
| `Lambda`       | Wraps arbitrary expressions in a layer       |

---

### 2. Convolutional Layers

| Layer             | Description                         |
| ----------------- | ----------------------------------- |
| `Conv1D`          | 1D convolution (time-series, text)  |
| `Conv2D`          | 2D convolution (images)             |
| `Conv3D`          | 3D convolution (volumetric data)    |
| `SeparableConv2D` | Depthwise separable 2D convolution  |
| `Conv2DTranspose` | Transposed (upsampling) convolution |
| `Cropping2D`      | Crops borders of 2D inputs          |
| `ZeroPadding2D`   | Pads with zeros around 2D input     |

---

### 3. Pooling Layers

| Layer                          | Description                  |
| ------------------------------ | ---------------------------- |
| `MaxPooling1D/2D/3D`           | Max pooling                  |
| `AveragePooling1D/2D/3D`       | Average pooling              |
| `GlobalMaxPooling1D/2D/3D`     | Global max over all elements |
| `GlobalAveragePooling1D/2D/3D` | Global average pooling       |

---

### 4. Recurrent Layers

| Layer             | Description                                 |
| ----------------- | ------------------------------------------- |
| `SimpleRNN`       | Basic recurrent unit                        |
| `LSTM`            | Long Short-Term Memory unit                 |
| `GRU`             | Gated Recurrent Unit                        |
| `RNN`             | Base class for custom recurrent units       |
| `Bidirectional`   | Wraps any RNN for bi-directional processing |
| `TimeDistributed` | Applies layer to every time step            |

---

### 5. Normalization Layers

| Layer                | Description                                |
| -------------------- | ------------------------------------------ |
| `BatchNormalization` | Normalizes activations per batch           |
| `LayerNormalization` | Normalizes across features                 |
| `GroupNormalization` | Normalizes groups of channels (via add-on) |
| `UnitNormalization`  | Normalizes inputs to unit norm             |

---

### 6. Embedding Layers

| Layer       | Description                                                          |
| ----------- | -------------------------------------------------------------------- |
| `Embedding` | Turns positive integers (token IDs) into dense vectors of fixed size |

---

### 7. Attention Layers

| Layer                | Description                              |
| -------------------- | ---------------------------------------- |
| `Attention`          | Basic additive attention                 |
| `AdditiveAttention`  | Bahdanau-style attention                 |
| `MultiHeadAttention` | Transformer-style attention (self/cross) |

---

### 8. Merging Layers

| Layer         | Description                       |
| ------------- | --------------------------------- |
| `Add`         | Element-wise addition             |
| `Subtract`    | Element-wise subtraction          |
| `Multiply`    | Element-wise multiplication       |
| `Average`     | Element-wise average              |
| `Maximum`     | Element-wise maximum              |
| `Concatenate` | Joins inputs along specified axis |
| `Dot`         | Computes dot product              |

---

### 9. Reshaping & Utility Layers

| Layer          | Description                   |
| -------------- | ----------------------------- |
| `Reshape`      | Changes shape                 |
| `Flatten`      | Flattens tensor               |
| `RepeatVector` | Repeats input n times         |
| `Permute`      | Rearranges axes               |
| `Lambda`       | Applies arbitrary expressions |

---

### 10. Preprocessing Layers (Structured & Text)

| Layer                  | Description                             |
| ---------------------- | --------------------------------------- |
| `Normalization`        | Standardizes inputs                     |
| `Discretization`       | Buckets continuous features             |
| `StringLookup`         | Converts string tokens to integer IDs   |
| `IntegerLookup`        | Converts integer tokens to dense format |
| `CategoryEncoding`     | One-hot, multi-hot encoding             |
| `TextVectorization`    | Tokenizes and vectorizes text           |
| `Rescaling`            | Scales pixel values (e.g., to \[0, 1])  |
| `CenterCrop`, `Resize` | Image resizing and cropping             |

---

## Custom Layers

### Creating a Custom Layer

```python
from tensorflow.keras.layers import Layer

class MyCustomLayer(Layer):
    def __init__(self, units):
        super(MyCustomLayer, self).__init__()
        self.units = units

    def build(self, input_shape):
        self.w = self.add_weight(shape=(input_shape[-1], self.units), initializer="random_normal")
        self.b = self.add_weight(shape=(self.units,), initializer="zeros")

    def call(self, inputs):
        return tf.matmul(inputs, self.w) + self.b
```

---

## Summary Table by Use Case

| Task                 | Recommended Layers                               |
| -------------------- | ------------------------------------------------ |
| Classification       | `Dense`, `Dropout`, `Activation`                 |
| Image Processing     | `Conv2D`, `MaxPooling2D`, `Flatten`, `BatchNorm` |
| Text Processing      | `Embedding`, `LSTM`, `GRU`, `TextVectorization`  |
| Sequence to Sequence | `LSTM`, `GRU`, `Attention`, `Bidirectional`      |
| Transformers         | `MultiHeadAttention`, `LayerNormalization`       |
| Structured Data      | `Normalization`, `StringLookup`, `Dense`         |

---
