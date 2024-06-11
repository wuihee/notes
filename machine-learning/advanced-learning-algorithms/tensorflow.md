# TensorFlow

## TensorFlow & NumPy

### NumPy Matrices

- 1 x 2 Matrix

    ```python
    np.array([[1, 2]])
    ```

- 2 x 1 Matrix

    ```python
    np.array([
        [1],
        [2],
    ])
    ```

- 1D Vector

    ```python
    np.array([1, 2, 3])
    ```

### TensorFlow Matrices

- Matrix representation

    ```python
    a1 = tf.Tensor([[0.2, 0.7, 0.3]], shape=(1, 3), dtype="float32")
    ```

- Conversion to NumPy array.

    ```python
    a1.numpy()
    ```

## TensorFlow Implementation Example

```python
# Input
x = np.array([200, 17])

layer_1 = Dense(units=3, activation="sigmoid")
a1 = layer_1(x)

layer_2 = Dense(units=1, activation="sigmoid")
a2 = layer_2(a1)
```

```python
model = Sequential(
    Dense(units=3, activation="sigmoid"),
    Dense(units=1, activation="sigmoid"),
)
model.compile(...)
model.fit(x, y)
model.predict(x_new)
```

## Forward Propagation

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

```python
def dense(A_in, W, B):
    Z = np.matmul(A_in, W) + B
    A_out = g(Z)
    return A_out
```
