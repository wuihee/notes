# Collaborative Filtering

## Making Recommendations

- A *recommender task* ... E.g. Predicting which movies users will prefer on a movie streaming platform.
- The dataset will contain a list of users and the items that each user has / hasn't rated.
  - $n_u$ - The number of users.
  - $n_m$ - The number of items.
  - $r(i, j)$ - Returns 1 if the $j^{th}$ user has rated the $i^{th}$ item, else 0.
  - $y^{(i, j)}$ - The rating given to the $i^{th}$ item by the $j^{th}$ user.

## Using Per-Item Features

- We can create a better recommender system if the items we are trying to predict for had their own features. E.g. In our movie recommendation example, the features for each movie could be their genre.
  - $n$ - The number of features each item has.
  - $\vec{x}^{(i)}$ - Feature vector for the $i^{th}$ item.
  - $\vec{w}^{(j)}$, $b^{(j)}$ - Parameters for the $j^{th}$ user.
  - $m^{(j)}$ - Number of movies rated by the $j^{th}$ user.
- To predict whether a user $j$ will like an item $i$, we can use a *linear regression* model:

$$w^{(j)} \cdot x^{(i)} + b^{(j)}$$

- To learn parameters $w^{(j)}$, $b^{(j)}$ for user $j$, we define our cost function $J$ as the mean of the sum of the mean squared error between the predicted rating, and the actual rating $y^{(i, j)}$:

$$J(w^{(j)}, b^{(j)}) = \frac{1}{2m^{(j)}} \sum_{i:r(i, j) = 1}(\vec{w}^{(j)} \cdot \vec{x}^{(i)} + b^{(j)} - y^{(i, j)})^2$$

- We can add the regularization term.

  $$J(w^{(j)}, b^{(j)}) = \frac{1}{2m^{(j)}} \sum_{i:r(i, j) = 1} (w^{(j)} \cdot x^{(i)} + b^{(j)} - y^{(i, j)})^2 + \frac{\lambda}{2m^{(j)}} \sum^{n}_{k = 1} (w_k^{(j)})^2$$

- Therefore, to learn parameters $w^{(n_u)}$, $b^{(n_u)}$ for all users:

$$J = \frac{1}{2} \sum^{n_u}_{j = 1} \sum_{i:r(i, j) = 1} (\vec{w}^{(j)} \cdot \vec{x}^{(i)} + b^{(j)} - y^{(i, j)})^2 \frac{\lambda}{2} \sum^{n_u}_{j = 1} \sum^n_{k = 1} (\vec{w}_k^{(j)})^2$$

## Collaborative Filtering Algorithm

- Assume we know the weights $\vec{w}^{(i)}$ and bias $b$. We can run through the weights for each user $j$ and estimate the feature vector for each item $\vec{x}^{(i)}$.
- Given $w^{(1)}$, $b^{(i)}$,..., $w^{(n_u)}$, $b^{(n_u)}$, to learn $x^{(i)}$, we can try to minimize the following cost function:

$$J(\vec{x}^{(i)}) = \frac{1}{2} \sum_{j:r(i, j) = 1} (\vec{w}^{(j)} \cdot \vec{x}^{(i)} + b^{(j)} - y^{(i, j)})^2 + \frac{\lambda}{2} \sum^n_{k = 1} (\vec{x}_k^{(i)})^2$$

- To learn the features for all the items $x^{(i)}$, ..., $x^{(n_m)}$, we can try to minimize the sum of the cost functions for each item, giving us a new cost function:

$$J(x^{(i)}, ..., x^{(n_m)}) = \frac{1}{2} \sum^{n_m}_{i = 1} \sum_{j:r(i, j) = 1} (\vec{w}^{(j)} \cdot \vec{x}^{(i)} + b^{(j)} - y^{(i, j)})^2 \frac{\lambda}{2} \sum^{n_m}_{i = 1} \sum^n_{k = 1} (\vec{x}_k^{(i)})^2$$

- To finish our collaborative filtering algorithm to learn $w^{(j)}$, $b^{(j)}$, and $x^{(i)}$ we can combine our previous 2 formulas:

$$J(w^{(j)}, b^{(j)}, x^{(i)}) = \sum_{(i, j):r(i, j) = 1} (\vec{w}^{(j)} \cdot \vec{x}^{(i)} + b^{(j)} - y^{(i, j)})^2 + \frac{\lambda}{2} \sum^{n_u}_{j = 1} \sum^n_{k = 1} (\vec{w}_k^{(j)})^2 + \frac{\lambda}{2} \sum^{n_m}_{i = 1} \sum^n_{k = 1} (\vec{x}_k^{(i)})^2$$

- The method to minimize our cost function is using gradient descent as always. However, since our cost function is a function of $w$, $b$, and $x$, we also need to include our $x$ term:

$$w_i^{(j)} = w_i^{(j)} - \alpha \frac{\partial}{\partial w_i^{(j)}} J(w, b, x)$$

$$b^{(j)} = b^{(j)} - \alpha \frac{\partial}{\partial b^{(j)}} J(w, b, x)$$

$$x_k^{(i)} = x_k^{(i)} - \alpha \frac{\partial}{\partial x_k^{(i)}} J(w, b, x)$$

## Binary Labels

- We can adapt collaborative filtering for the scenario where instead of a user's rating, we want binary labels, meaning the user either "likes" or "dislikes" an item.
  - "Liking" / "disliking" an item refers refers to whether the user engaged with the item.
  - E.g. Did user $j$ click / purchase / like the item in question?
- Meaning of ratings:
  - 1 - Engaged with after showing the item.
  - 0 - Did not engage with the item.
  - ? - Did not see the item.

### From Regression to Binary Classification

- Previously, rating $y^{(i, j)} = \vec{w}^{(j)} \cdot \vec{x}^{(i)} + b^{(j)}$.
- For binary labels, the prediction that the probability of $y^{(i, j)} = 1$ is given by $g(\vec{w}^{(j)} \cdot \vec{x}^{(i)} + b^{(j)})$, where $g(z) = \Large \frac{1}{1 + e^{-z}}$ (i.e. logistic regression).

### Cost Function for Binary Application

- Loss function for single example:

$$L(f_{\vec{w}, b, \vec{x}}(\vec{x}), y^{(i, j)}) = -y^{(i, j)}\log (f_{\vec{w}, b, \vec{x}}(\vec{x})) - (1 - y^{(i, j)})\log (1 - f_{\vec{w}, b, \vec{x}}(\vec{x}))$$

- Cost function for binary application:

$$J(\vec{w}, b, \vec{x}) = \sum_{(i, j): r(i, j) = 1} L(f_{\vec{w}, b, \vec{x}}(\vec{x}), y^{(i, j)})$$

## Mean Normalization

- In the case where we have a new user who hasn't made any ratings, our regularization terms will try to minimize their weights, making it 0. As a result, all of their predictions will be 0.
- We can use *mean normalization* to allow our algorithm to give new users better predictions.
- Let $\vec{\mu}$ be the average rating of each item. We can then normalize all ratings by subtracting $\vec{\mu}$ from them.
- As such, to predict movie $i$ for user $j$, our new formula is $w^{(j)} \cdot x^{(i)} + b^{(j)} + \mu_i$ because we can't have negative predictions.
- As a result, for new users, when $w^{(j)} = 0$ and $b^{(j)} = 0$, $y^{(i, j)} = \mu_i$ which is a more reasonable estimate.

## Finding Related Items

- To find other items related to item $i$, we can find item $k$ with features $\vec{x}^{(k)}$ similar to $\vec{x}^{(i)}$.
- We can determine the similarity between items by finding the squared distance between the item's feature vectors:

$$\sum^n_{l = 1} (x_l^{(k)} - x_l^{(i)})^2 = ||x_l^{(k)} - x_l^{(i)}||^2$$

## TensorFlow Implementation

- We have to implement a custom training loop for collaborative filtering. However, TensorFlow's API allows us to automatically calculate the gradient of our cost function.

    ```python
    import tensorflow as tf
    from tensorflow import keras

    W = tf.Variable(tf.random.normal((num_users, num_features), dtype=tf.float64), name="W")
    X = tf.Variable(tf.random.normal((num_movies, num_features), dtype=tf.float64), name="X")
    b = tf.Variable(tf.random.normal((1, num_users), dtype=tf.float64), name="b")

    optimizer = keras.optimizers.Adam(learning_rate=1e-1)
    epochs = 200
    lambda_ = 1
    for _ in range(epochs):
        with tf.GradientTape() as tape:
            cost_value = cost_func(X, W, b, Y_norm, R, lambda_)

        # Use the gradient tape to automatically retrieve the gradients of the
        # trainable variables with respect to the loss.
        gradients = tape.gradient(cost_value, [X, W, b])

        # Run one step of gradient descent by updating the value of the variables
        # to minimize the loss.
        optimizer.apply_gradients(zip(gradients), [X, W, b])

    # Make predictions.
    p = np.matmul(X.numpy(), W.numpy().T) + b.numpy()
    
    # Restore the mean.
    pm = p + Y_mean
    ```
