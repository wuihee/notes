# Tree Ensembles

## Using Multiple Decision Trees

- A single decision tree is not very robust, and its structure (i.e. how it chooses which features to split on), can very easily be different with a change in a single training example.
- Tree Ensemble: Therefore, we can use multiple different decision trees, run our data through all of them, and classify our label with the one that got the most “votes”.

## Sampling with Replacement

- Sampling with replacement is the process of taking a sample from your dataset, but with every example you take out, you put it back into the sampling pool.
- This is to ensure that there are some variations in different samples.
- With this, we can construct slightly different datasets to train our decision tree ensemble on.

## Random Forest Algorithm

- We can introduce *sampling with replacement* on our dataset of size $m$, $B$ number of times, where $B$ will be the number of decision trees in our *random forest*.
  - This technique of creating a decision tree with sampling with replacement is called a *bagged decision tree*.
  - A good value for $B$ would range between 64 and 128.

### Randomizing the Feature Choice

- A problem is that a lot times, our decision trees end up looking very similar.
- Therefore, at each node if we have $n$ features to choose from to split on, pick a feature from a smaller subset of $k$ features, where $k < n$.
  - Typically, $k = \sqrt{n}$

## XGBoost

- XGBoost is the preferred tree ensemble algorithm which instead of sampling with replacement, assigns weights to examples. This makes it more likely for training examples that were misclassified by earlier decision trees to be chosen.

  ```python
  from xgboost import XGBClassifier

  model = XGBClassifier()

  model.fit(X_train, y_train)
  y_pred = model.predict(X_test)
  ```

## When to Use Decision Trees

### Decision Tree Considerations

- Works well with structured / tabular data, like an excel sheet.
- Not good with unstructured data (e.g. audio, images, text).
- Small decision trees have the advantage of being human interpretable.

### Neural Network Considerations

- Works well with all data.
- Slower than decision trees.
- Works with transfer learning.
- When building a system with multiple models working together, it may be easier to string together neural networks than decision trees.
