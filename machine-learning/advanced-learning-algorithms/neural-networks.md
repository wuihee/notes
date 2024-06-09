# Neural Networks

## Intuition

- Why do we need neural networks when we have traditional machine learning algorithms? That's because as the size of our data increases, the effectiveness of traditional models don't increase that much. However, huge amounts of data make neural networks very effective.
- Artificial neural networks take inspiration from biological neural networks, where networks consist of layers and neurons. neurons are basically *activation functions* which takes an input and produces an output. Layers are a group of neurons, which together, produce a vector output given a vector input.
- The first layers is called the input layer, where we are given a vector of feature inputs. This vector is passed through subsequent hidden layers - the vector input from the previous layer is passed through each neuron.
- Each neuron is a logistic regression sigmoid function which produces a new value.
- After everything is passed through all the hidden layers, we arrive at our final output layer with a single value. This value can be converted to a boolean using a 0.5 threshold value.
- Determining the number of layers and neurons for our model is part of model architecture.

## How does this work in qualitatively?

- Let's say we are trying to predict if a new t-shirt is going to be a hit.
- Our input features are: price, production cost, marketing, and material.
- We think that the features which determine a hit are: affordability, awareness, and perceived quality, each of which we represent with a neuron, and group together in a layer.
- We pass our initial input: [price, production cost, marketing, material] into the next layer.
- Looking at the 'affordability' feature, our network will automatically determine which parameters among our input to place importance on. In contrast, for traditional machine learning algorithms, we manually engineer the features.

## Notation

- $\vec{x}$ - Our input features.
- $g(z) = \frac{1}{1 + e^{-z}}$ - Sigmoid function.
- $\vec{a}^{[l]}$ - Activation / output vector for the $l^{th}$ layer.
- $a^{[l]}_j$ - For the $l^{th}$ layer, the $j^{th}$ neuron's activation /output value.
- $a^{[l]}_j = g(\vec{w}^{[l]} \cdot \vec{a}^{[l - 1]} + b^{[l]}_j)$ - The activation value of the $l^{th}$ layer and the $j^{th}$ value is the sigmoid function of the dot product of the parameters for the $l^{th}$ layer and activation results of the previous layer, plus the bias.

## TensorFlow Implementation Example

```python
# Input
x = np.array([200, 17])

layer_1 = Dense(units=3, activation="sigmoid")
a1 = layer_1(x)

layer_2 = Dense(units=1, activation="sigmoid")
a2 = layer_2(a1)
```
