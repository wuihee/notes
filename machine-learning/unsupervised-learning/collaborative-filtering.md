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
