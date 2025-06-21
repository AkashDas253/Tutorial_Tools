## High-Level API in Keras

The Keras High-Level API provides a user-friendly interface for building machine learning models, allowing you to focus on architecture design rather than low-level implementation details. It consists of three main approaches: the Sequential API, the Functional API, and Model Subclassing.

---

#### Overview of High-Level APIs

| **API**           | **Description**                                                                                   | **Use Cases**                                                                                 |
|--------------------|---------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| Sequential API     | Simplifies the creation of linear stack models where each layer has one input and one output.     | Simple feedforward networks or prototypes.                                                   |
| Functional API     | Enables the construction of complex architectures like multi-input/output and shared layers.      | Advanced architectures such as ResNet, UNet, or models with branching structures.            |
| Model Subclassing  | Allows complete customization by subclassing `tf.keras.Model` and defining your forward pass.     | Research experiments or models requiring highly specific or unconventional architectures.     |

---

### **1. Sequential API**

- **Description**: 
  The Sequential API is a linear stack of layers. It is simple to use and suitable for beginner-friendly tasks or straightforward architectures.

- **Key Features**:
  - Easy to implement.
  - Layers are stacked in a sequence.
  - No flexibility for complex architectures like branching.

- **Example Usage**:
  ```python
  from tensorflow.keras import Sequential
  from tensorflow.keras.layers import Dense, Flatten

  model = Sequential([
      Flatten(input_shape=(28, 28)),
      Dense(128, activation='relu'),
      Dense(10, activation='softmax')
  ])
  model.summary()
  ```

---

### **2. Functional API**

- **Description**:  
  The Functional API offers flexibility to build directed acyclic graphs of layers, making it suitable for more advanced architectures.

- **Key Features**:
  - Supports multiple inputs and outputs.
  - Enables reuse of layers and shared weights.
  - Visual clarity of architecture.

- **Key Concepts**:
  
  | **Concept**              | **Description**                                                                                         |
  |--------------------------|---------------------------------------------------------------------------------------------------------|
  | Inputs                  | Define the input shape using `Input`.                                                                    |
  | Layers                  | Connect layers by treating them as functions.                                                           |
  | Outputs                 | Specify final outputs to complete the model.                                                            |

- **Example Usage**:
  ```python
  from tensorflow.keras import Model, Input
  from tensorflow.keras.layers import Dense, concatenate

  # Define inputs
  input1 = Input(shape=(32,))
  input2 = Input(shape=(16,))

  # Define layers
  x1 = Dense(64, activation='relu')(input1)
  x2 = Dense(64, activation='relu')(input2)
  merged = concatenate([x1, x2])

  # Outputs
  output = Dense(10, activation='softmax')(merged)

  # Model
  model = Model(inputs=[input1, input2], outputs=output)
  model.summary()
  ```

---

### **3. Model Subclassing**

- **Description**:  
  Model Subclassing provides the greatest flexibility by letting you define your custom model class, overriding the `call` method for forward propagation.

- **Key Features**:
  - Full control over forward pass and dynamic behavior.
  - Suitable for non-standard architectures or research use.

- **Example Usage**:
  ```python
  from tensorflow.keras import Model
  from tensorflow.keras.layers import Dense

  class CustomModel(Model):
      def __init__(self):
          super(CustomModel, self).__init__()
          self.dense1 = Dense(64, activation='relu')
          self.dense2 = Dense(10, activation='softmax')

      def call(self, inputs):
          x = self.dense1(inputs)
          return self.dense2(x)

  model = CustomModel()
  model.build(input_shape=(None, 32))
  model.summary()
  ```

---

#### Comparison Table for High-Level APIs

| **Feature**                | **Sequential API**              | **Functional API**              | **Model Subclassing**            |
|----------------------------|----------------------------------|----------------------------------|----------------------------------|
| **Ease of Use**            | Very simple, beginner-friendly  | Moderate complexity             | Advanced, requires coding skills |
| **Flexibility**            | Low                             | High                            | Maximum                          |
| **Model Complexity**       | Linear stacks only              | Any directed acyclic graph       | Fully customizable               |
| **Reusability**            | Minimal                         | Moderate                        | High                             |
| **Best Use Case**          | Simple prototypes               | Complex architectures           | Research/customized models       |

---

#### Key Usage Notes

- **When to Use**:
  - Start with **Sequential API** for simple models and beginner tasks.
  - Move to **Functional API** for complex architectures or shared weights.
  - Use **Model Subclassing** when designing highly customized models.
