# Decision Trees

## Decision Tree Model

- A decision tree model helps with classification tasks.
- A decision tree is created out of the features of the data. To classify an example, we start from the *root node*, move left or right down the tree’s *decision nodes* based on the current example’s features, and arrive at a *leaf node* which classifies the example.
- For example, we are trying to classify whether an animal is a cat. Features include, pointy/round ears, whiskers, and face shape. We move down the tree left/right depending on whether our animal has pointy/round ears etc.
- The goal of the decision tree model is to choose one that best classifies our data.

## Learning Process

- **Decision 1**: How do we decide how to construct our tree, i.e. which features do we split on?
  - A high level of purity refers to the state where all labels on a node are of the same class.
  - Therefore, split on features which maximize purity.
- **Decision 2**: When do we stop splitting our decision tree?
  - Specify a certain depth, where the depth of a tree at a node refers to the number of hops it takes to get there.
  - Specify a level of purity to stop splitting.
  - When the number of examples in a node is below a certain threshold.
  - The purpose of this decision is to keep the tree small and reduce over-fitting.
