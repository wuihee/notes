# TensorFlow

## TensorFlow & NumPy

### NumPy Matrices

## Forward Propagation

- We can manually pass the outputs from each layer to the next layer.

    ```python
    x = np.array([200, 17])

    layer_1 = Dense(units=3, activation="sigmoid")
    a1 = layer_1(x)

    layer_2 = Dense(units=1, activation="sigmoid")
    a2 = layer_2(a1)
    ```

- Or, we can use `Sequential`.

    ```python
    model = Sequential(
        Dense(units=3, activation="sigmoid"),
        Dense(units=1, activation="sigmoid"),
    )
    ```

### `Dense` and `Sequential`

- Without vectorization.

    ```python
    def dense(a_in, W, b):
        units = W.shape()[1]
        a_out = np.zeros(units)
        for j in range(units):
            w = W[:, j]
            z = np.dot(w, a_in) + b[j]
            a_out[j] = g(z)  # Sigmoid function
        return a_out


    def sequential(x):
        a1 = dense(x, W1, b1)
        a2 = dense(a1, W2, b2)
        return a2
    ```

- With vectorization.

    ```python
    def dense(A_in, W, B):
        Z = np.matmul(A_in, W) + B
        A_out = g(Z)
        return A_out
    ```

### Notes

- Normalization layer
- 'Adapt' data

    ```python
    normal_layer = tf.keras.layers.Normalization(axis=-1)
    normal_layer.adapt(X)
    Xn = normal_layer(X)
    ```

- Specify input shape. Usually TensorFlow does this automatically.

    ```python
    tf.keras.Input(shape=(2,))
    ```

- Summarize model.

    ```python
    model.summary()
    ```

- Use `model.compile` to define a loss function and compile optimization.
- `model.fit` runs gradient descent to fit the weights to the data.

    ```python
    model.compile(
        loss=tf.keras.losses.BinaryCrossentropy(),
        optimizer=tf.keras.optimizers.Adam(learning_rate=0.01)
    )
    model.fit(Xt, Yt, epochs=10)
    ```

- When using the model to make predictions, we must also normalize our data.

    ```python
    X_testn = normal_layer(X_testn)
    predictions = model.predict(X_testn)
    ```

### Broadcasting

- NumPy broadcasting allows you to "stretch" smaller items so that operations can be performed on them with larger matrices.
- What is reshape(-1, 1)?
