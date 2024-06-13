# Neural Network Training

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

## Activation Functions

- For our output layer, choose the activation function based on the type of problem. For example, for classification problems, choose the sigmoid activation, and for regression problems, the linear or reLU activation.
- However, for hidden layers, default to reLU.

- Linear / No Activation: $g(z) = z$
- Sigmoid: $g(z) = \frac{1}{1 + e^{-z}}$
- ReLU: $g(z) = max(0, z)$

### Hidden Layers

- ReLU is less computationally expensive than the sigmoid function.
- Additionally, because of the shape of its graph, gradient descent is more effective.

### Why Use Activation Functions?

- If we use the linear activation function for every neuron, the end product will just be a linear regression model, making our neural network pointless.
