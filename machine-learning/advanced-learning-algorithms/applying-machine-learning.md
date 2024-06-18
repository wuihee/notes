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
