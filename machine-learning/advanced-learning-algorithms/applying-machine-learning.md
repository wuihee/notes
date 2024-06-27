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

### Error Analysis

- Error analysis is the process of manually going through your training examples, classifying them, and figuring out which your model did poorly on.
- This way, you know which categories of data your model is weak in and you know which areas to prioritize your time.

### Adding Data

- After error analysis, we can improve the areas the model is weak in by adding more data with different techniques.
- **Data Augmentation**: Modify existing data and add them as new examples. E.g., for an image classification task, we can rotate, skew, or distort images.
- **Data Synthesis**: Create new examples from scratch. E.g. for a model which reads text, we can generate examples by creating images with different fonts and background colors.

### Transfer Learning

- Transfer learning is a technique used to improve a model's performance, where we first pre-train our model on an existing dataset, and then fine-tune it on our current dataset.
  - We can either keep the parameters and only fine-tune the output layer.
  - Or, we can fine-tune all layers.
- The intuition behind transfer learning is that by pre-training our model, we give it a good starting point. E.g. for an image classification task, the initial hidden layers of the model learn to recognize very basic shapes and contours which are universal for all image recognition.
- Furthermore, there are already many pre-trained neural networks that can be used as a starting point.
- However, transfer learning only works for models of the same tasks. E.g. We need to pre-train with images for a computer vision task.

### Full Cycle of a Machine Learning Project

1. Scope Project
2. Collect Data
3. Train Model
4. Deployment
   - Host on an *inference server* where your application can make API calls to.

## Skewed Datasets

### Error Metrics for Skewed Datasets

- Sometimes, a model's accuracy alone isn't a sufficient analysis of the model's performance.
  - E.g. We have a model that classifies a rare disease with 99% accuracy which appears impressive.
  - However, if the disease only appears in 0.5% of the population, if we had a model which simply print "no disease" every time, our accuracy would be at 99.5%.
- We can use a *confusion matrix* to represent the accuracy of the model:

  |  Actual  |      Positive       |      Negative       |
  |----------|---------------------|---------------------|
  | Positive | True Positive (TP)  | False Negative (FN) |
  | Negative | False Positive (FP) | True Negative (TN)  |

- **Precision**: Of examples that were predicted to be positive, how many were actually positive?

  $precision = \frac{TP}{TP + FP}$

- **Recall**: Of examples that were actually positive, how many were accurately predicted?

  $recall = \frac{TP}{TP + FN}$

### Precision / Recall Tradeoff

- Often, we need to find a tradeoff between precision and recall.
  - E.g. If our rare disease is extremely deadly, we would want a high level of recall, because we wouldn't want to miss out on any cases.
  - On the other hand, if our rare disease is mild, we would go for a high precision, so that we only bother the patient when we know for sure they have the disease.
- We can prioritize precision / recall by adjusting a threshold with which we use for our classification.
  - If we set a high threshold (e.g. 0.9), our algorithm will be very precise and correctly identify almost all the examples. However, it may miss out on many.
  - However, if we set a low threshold (e.g. 0.1), our algorithm will have a high recall. It will catch almost all the correct examples, but also produce a lot of false positives.
- The $F1 score$ is a way to combine precision and recall values, to provide a single number which to evaluate our model. It uses a *harmonic mean* to give more emphasis to lower values.

  $F_1 = \frac{1}{\frac{1}{2}(\frac{1}{P} + \frac{1}{R})}$\
  $F_1 = \frac{2PR}{P + R}$
