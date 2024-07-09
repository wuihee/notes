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
  - $\vec{w}^{(j)}$, $b^{(j)}$ - Parameters for the $j^{th}$ user.
  - $\vec{x}^{(i)}$ - Feature vector for the $i^{th}$ item.
  - $m^{(j)}$ - Number of movies rated by the $j^{th}$ user.
- To predict for

$w^{(j)} \cdot x^{(i)} + b^{(j)}$

$\text{min}_{w^{(j)}, b^{(j)}} \{J(w^{(j)}, b^{(j)})\} = \frac{1}{2m^{(j)}} \sum_{i:r(i, j) = 1} (w^{(j)} \cdot x^{(i)} + b^{(j)} - y^{(i, j)})^2$
