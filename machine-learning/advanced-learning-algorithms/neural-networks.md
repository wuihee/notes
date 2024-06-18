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

### Terminology

- **Neuron** - A single unit which accepts a vector input and runs it through an activation function.
- **Activation** - The function which a neuron computes on an input.
- **Feature Vector** - The input vector, where each value in the vector corresponds to the value of its respective feature.
- **Layer (Input, Hidden, Output)** - A group of neurons consist of a layer in the neural network which outputs a vector.
- **Forward Propagation** - The process of forwarding the output vectors of each layer to the next.

### Machine vs Deep Learning

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

## Neural Network Training

- Define a model by building the layers.

    ```python
    Sequential(
        Dense(25, activation="sigmoid"),
        Dense(15, activation="sigmoid"),
        Dense(1, activation="sigmoid"),
    )
    ```

- Specify the loss function.

    ```python
    model.compile(loss=BinaryCrossentropy())
    ```

- Run gradient descent on the model to fit the data.

    ```python
    model.fit(X, y, epochs=100)
    ```

### Activation Functions

- For our output layer, choose the activation function based on the type of problem. For example, for classification problems, choose the sigmoid activation, and for regression problems, the linear or reLU activation.
- However, for hidden layers, default to reLU.

- Linear / No Activation: $g(z) = z$
- Sigmoid: $g(z) = \frac{1}{1 + e^{-z}}$
- ReLU: $g(z) = max(0, z)$

### Hidden Layers

- ReLU is less computationally expensive than the sigmoid function.
- Additionally, because of the shape of its graph, gradient descent is more effective.
- It's ability to "turn-off" allows the neural network to "stitch together" different linear functions to create complex graphs to fit the model.

### Why Use Activation Functions?

- If we use the linear activation function for every neuron, the end product will just be a linear regression model, making our neural network pointless.

## Adam Algorithm

- A more efficient way to train neural networks instead of using gradient descent.
- The general ideas is that if our gradient descent is moving in a consistent direction, we can speed up the learning rate $\alpha$, or slow it down if it's jumping around.

    ```python
    model.compile(
        optimizer=tf.keras.optimizers.Adam(learning_rate=1e-3),
        loss=tf.keras.losses.SparseCategoricalCrossentropy(from_logits=True)
    )
    ```
