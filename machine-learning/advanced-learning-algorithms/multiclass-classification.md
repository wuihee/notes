# Multiclass Classification

## Softmax

While logistic regression predicts for a binary classification, softmax classifies for multiple classes. E.g. recognizing different handwritten digits in the MNST dataset.

- Recall for logistic regression, where $a_1$ and $a_2$ are the probabilities of the classification problem:

    $z = \vec{w} \cdot \vec{x} + b$\
    $a_1 = g(z) = \frac{1}{1 + e^{-z}}$\
    $a_2 = 1 - a_1$

- Softmax regression, for each category $j$, where $a_j$ is the probability for the $j^{th}$ category and $L$ is the loss function:

    $z_j = \vec{w_j} \cdot \vec{x} + b_j$\
    $a_j = \frac{e^{z_j}}{\sum^{N}_{k=1} e^{z_k}} = P(y = j | \vec{x})$\
    $L(a_1, ..., a_N, y) = -\log a_N$ if $y = N$\
    Where, $a_1 + a_2 + ... + a_N = 1$

- To use a softmax activation, we specify it for our final ouput layer. The number of units in our output layer will equal to the number of categories we have.

    ```python
    model = Sequential([
        Dense(units=25, activation='relu'),
        Dense(units=15, activation='relu'),
        Dense(units=10, activation='softmax')
    ])
    model.compile(loss=SparseCategoricalCrossEntropy())
    model.fit(X, Y, epochs=100)
    ```

## Reducing Numerical Roundoff Errors

When computing complex mathematical operations, numerical roundoff errors may occur. We can mitigate this by reducing the number of intermediary mathematical operations.

- Logistic Regression: We can change our final activation layer to a linear activation and slightly modify our loss function.

    ```python
    model = Sequential([
        Dense(units=25, activation='relu'),
        Dense(units=15, activation='relu'),
        Dense(units=1, activation='linear')
    ])
    model.compile(loss=BinaryCrossEntropy(from_logits=True))
    model.fit(X, Y, epochs=100)
    ```

- Originally, our loss function is defined by:

    $a = g(z) = \frac{1}{1 + e^{-z}}$\
    $L = -y \log (a) - (1 - y)\log (1 - a)$

- But afterwards, we reduce the intermediary steps so that:

    $L = -y \log (\frac{1}{1 + e^{-z}}) - (1 - y)\log (1 - \frac{1}{1 + e^{-z}})$

- For softmax, we can apply the same technique:

    ```python
    model = Sequential([
        Dense(units=25, activation='relu'),
        Dense(units=15, activation='relu'),
        Dense(units=1, activation='linear')
    ])
    model.compile(loss=SparseCategoricalCrossEntropy(from_logits=True))
    model.fit(X, Y, epochs=100)
    ```

- Finally, because our output layer we combine the steps for our loss function, we need to pass our result through a sigmoid function to get our predictions.

    ```python
    logit = model(X)
    f_x = tf.nn.sigmoid(logit)
    ```

## Multi-Label Classification

- For some scenarios like computer vision, we want to detect for multiple labels. For example, buses, cars, pedestrians, etc.
- We can do this by having our output layer consist of a separate neuron for each distinct label we want to classify.
