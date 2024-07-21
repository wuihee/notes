# Content-Based Filtering

## Collaborative Filtering vs Content-Based Filtering

- In collaborative filtering, items are recommended based on how you rate items and how others rated similar items.
- In content-based filtering, items are recommended based on the features of each user and each item.
  - $\vec{x}_u^{(j)}$ - Feature vector for user $j$.
  - $\vec{x}_m^{(i)}$ - Feature vector for movie (item) $i$.
- To predict a user’s rating for a given item, we can take a subset of the user’s features and a subset of the movie’s features and find the dot product between these two vectors, $\vec{v}_u^{(j)} \cdot \vec{v}_m^{(i)}$. Note that these vectors must be of the same length.

## Deep Learning for Content-Based Filtering

- To create our prediction feature vectors $\vec{v}_u^{(j)}$ and $\vec{v}_m^{(i)}$, we can run our original user and item feature vectors $\vec{x}_u^{(j)}$ and $\vec{x}_m^{(i)}$ through a neural network.
- To adapt our use case for binary labels we can pass our prediction through a sigmoid function, $g(\vec{v}_u \cdot \vec{v}_m)$ to predict the probability that $y^{(i, j)} = 1$.
- The network will try to minimize the cost function which finds the difference between the prediction and the actual item rating.

$$J = \sum_{(i, j):r(i, j) = 1} (\vec{v}_u^{(j)} \cdot \vec{v}_m^{(i)} - y^{(i, j)})^2$$

- This is one example of how it is easy to combine different neural networks.
- Content-based filtering can be computationally expensive.

## Recommending From a Large Catalogue

1. Retrieval
   - Generate a large list of possible candidates to recommend to the user.
2. Ranking
   - Rank the list of items based on the model.
   - Retrieving more items will result in better recommendations, but slower performance.
   - Do offline tests to find the best tradeoff.

## TensorFlow Implementation

```python
import tensorflow as tf

user_NN = tf.keras.models.Sequential([
    tf.keras.layers.Dense(256, activation="relu"),
    tf.keras.layers.Dense(128, activation="relu"),
    tf.keras.layers.Dense(32),
])

item_NN = tf.keras.models.Sequential([
    tf.keras.layers.Dense(256, activation="relu"),
    tf.keras.layers.Dense(128, activation="relu"),
    tf.keras.layers.Dense(32),
])

# Create user input vector and point to base network.
input_user = tf.keras.layers.Input(shape=(num_user_features))
vu = user_NN(input_user)
vu = tf.linalg.l2_normalize(vu, axis=1)

# Create item input vector and point to base network.
input_item = tf.keras.layers.Input(shape=(num_item_features))
vm = item_NN(input_item)
vm = tf.linalg.l2_normalize(vm, axis=1)

# Measure the similarity between the two vector outputs.
output = tf.keras.layers.Dot(axes=1)([vu, vm])

# Specify inputs and outputs of the model.
model = Model([input_user, input_item], output)

# Specify the cost function.
cost_fn = tf.keras.losses.MeanSquaredError()
```
