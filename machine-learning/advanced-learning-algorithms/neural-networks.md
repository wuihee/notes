# Neural Networks

## Introduction

### Example Problem

- Predict whether a newly released T-shirt will be a success.
- **Input Features**: Price, Production Cost, Marketing, Material
- **Predictive Features**: Affordability, Awareness, Perceived Quality

### Example Model

- The initial *input layer* consists of a vector containing the input features.
- This input layer is passed into the next *hidden layer* consisting of 3 neurons, each representing a predictive feature.
- Each neuron is essentially a sigmoid function, which takes the input vector as an argument and produces a new value. The values created by the neurons in the current layer are then treated as the input vector for the next layer.
- For example, the neuron representing 'affordability' might place emphasis on the 'price' and 'production cost' input features and less emphasis on the other features.
- In general, determining the number of neurons and layers is part of model architecture.

### Todo: Visualization

### Terminology

- Neuron
- Feature Vector
- Layer (Input, Hidden, Output)
- Activation

### Machine Learning vs Deep Learning

- As the size of available data increases, traditional machine learning algorithms don't improve in their effectiveness as much as neural networks do.
- In deep learning algorithms, features are automatically given importance as compared to traditional algorithms where features are manually engineered.

## Notation

- $\vec{x}$ - Input vector.
- $\vec{w}, b$ - Model parameters; weights and bias.
- $\vec{w}^{[l]}_j, b^{[l]}_j$ - Model parameter's for the $j^{th}$ neuron in the $l^{th}$ layer.
- $\vec{a}^{[l]}$ - Activation / output vector for the $l^{th}$ layer.
- $a^{[l]}_j$ - Activation value for the $j^{th}$ neuron in the $l^{th}$ layer.

## Formulas

### Sigmoid Function

Each neuron applies a sigmoid function to its given input.

$g(z) = \frac{1}{1 + e^{-z}}$

$z = \vec{w} \cdot \vec{x} + b$

### Activation Value

The activation value for the $j^{th}$ neuron of the $l^{th}$ layer is given by the sigmoid function of the dot product between the current weights and the activation results of the previous layer, plus the bias.

$a^{[l]}_j = g(\vec{w}^{[l]}_j \cdot \vec{a}^{[l - 1]} + b^{[l]}_j)$

## TensorFlow Implementation Example

```python
# Input
x = np.array([200, 17])

layer_1 = Dense(units=3, activation="sigmoid")
a1 = layer_1(x)

layer_2 = Dense(units=1, activation="sigmoid")
a2 = layer_2(a1)
```
