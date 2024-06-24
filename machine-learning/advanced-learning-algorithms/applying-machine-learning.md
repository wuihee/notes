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

### Learning Curves

- We can use a learning curve to evaluate a model's performance. A learning curve plots the amount of data the model is trained on to its performance.
- For a model with high bias, adding more data is not helpful, because you can only do so much with a simple model.
- However, for a model with high variance, adding more data can allow your model to create more accurate fits.

### Debugging

- For models with high variance:
  - Reduce features
  - Get more data
  - Reduce $\lambda$
- For models with high bias
  - Increase features
  - Add polynomial features
  - Increase $\lambda$

### Bias & Variance in Neural Networks

- Neural networks resolve the bias-variance tradeoff dilemma faced in traditional machine learning algorithms.
- Neural networks are often low-bias because they can fit complicated functions.
- A simple formula for training a neural network is to repeatedly increase its complexity via hidden layers/units until it does well on the training data. Afterwards, repeatedly feed it more training data until it does well on the cross-validation data.
- Additionally, we don't need to worry about overfitting for large neural networks as long as the regularization is chosen well.

    ```python
    model = Sequential(
        Dense(units=25, activation="relu", kernel_regularizer=L2(0.01))
        Dense(units=15, activation="relu", kernel_regularizer=L2(0.01))
        Dense(units=1, activation="sigmoid", kernel_regularizer=L2(0.01))
    )
    ```

## Machine Learning Development
