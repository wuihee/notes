# Applying Machine Learning

## Evaluating a Model

- Use a train-test split.
- When evaluating the cost of the model, we don't use the regularization term.
  - $J_{train}(\vec{w}, b)$ - How well the model performs on the training set.
  - $J_{test}(\vec{w}, b)$ - How well the model performs on the training set.

## Model Selection

- Use a 60-20-20 split for a train, cross-validation, and test set.
- Train the model on the train set.
- Choose the model with the lowest error on the cross-validation set.
- Evaluate the model's error with the test set.

## Bias & Variance

- A model with high bias (under-fitting) does poorly on the training set and on the cross-validation set.
- A model with high variance (over-fitting) does well on the training set but a lot worse on the cross-validation set.

### Regularization

- A small $\lambda$ value leads to high variance (over-fitting).
- A large $\lambda$ value leads to high bias (under-fitting).
