# Clustering

- Clustering is grouping together similar data points.
- In a machine learning context, we might want to apply clustering algorithms to find patterns given a bunch of unlabelled data points.

## K-Means Intuition

- *K-Means* is a clustering algorithm.
- First, specify the number of clusters to find.
- The algorithm then randomly assign locations for the *cluster centroids*.
- Continuously repeat these 2 steps until the algorithm converges:
  - Group each data point to its closest cluster centroid.
  - Move the cluster centroid to the average location of the points associated with it.

## K-Means Algorithms

- Randomly initialize $K$ cluster centroids, $\mu_1, \mu_2, ..., \mu_k$  (which have the same dimensions as your training examples).
- Next, we assign each point to the closest cluster centroid.
  - Let $c^{(i)}$ be the index of the cluster centroid with the closest squared distance to the point $x^{(i)}$.
  - $min_k \Vert x^{(i)} - \mu_k \Vert^2$.
- For $k = 1$ to $K$, Move the location of each cluster centroid to the *average position* of the the points assigned to it.
  - Let $\mu_k$ be the average of points assigned to cluster $k$.
- In the edge case where there are no points assigned to a cluster, the most common approach is to delete that cluster.
- K-means can also be applied to datasets that are not well separated.
  - E.g. if we have an un-clustered, continuous dataset of heights, we may use K-means to find clusters to create small, medium, and large categories.

## Optimization Objective

- $c^{(i)}$ - Index of the cluster $k$ which example $x^{(i)}$ is currently assigned.
- $\mu_k$ - Cluster centroid $k$.
- $\mu_{c^{(i)}}$ - Cluster centroid to which example $x^{(i)}$ has been assigned.

### Cost Function for K-Means

- **Cost / Distortion Function**: The average squared distance between every point and its cluster centroid.

    $J(c^{(1)}, ..., c^{(m)}, \mu_1, ..., \mu_k) = \frac{1}{m} \sum^{m}_{i = 1} \Vert x^{(i)} - \mu_{c^{(i)}} \Vert^2$

- When we assign points to cluster centroids, we are trying to keep  $\mu_1, ..., \mu_k$ fixed and minimize $J$.
- Likewise, by moving the cluster centroids to the average of its points, we are keeping $c^{(i)}, ..., c^{(m)}$ fixed while minimizing $J$.

## Initializing K-Means

- To select our cluster centroids:
  - Choose $K < m$.
  - Randomly pick $K$ training examples and set $\mu_1, ..., \mu_k$ equal to these examples.
- One problem that will be encountered for randomly assigning cluster centroids is that they may converge at non-optimal locations - in other words, our cost function $J$ will reduce to the local minimum and not the absolute minimum.
- To fix this, we should run K-means 50-1000 times and choose the result with the lowest cost function.

## Choosing the Number of Clusters

- Elbow Technique: Plot a cluster-cost graph and choose the number of clusters at the sharpest “elbow”. A little arbitrary and may not be effective.
- Instead, choose the number of clusters based on how well they perform on your (downstream) later purpose.
