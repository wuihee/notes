# Kruskal's Algorithm

- Sort the edges by edge weights in increasing order.
- Repeatedly add edges until all nodes are covered.

## Time Complexity

- $\Theta(N \lg N)$

## Disjoint Sets

- Individual components are *disjoint sets* that can be implemented with *union find*.
- If vertices $v$ to $w$ are in the same set, then adding it would create a cycle. Otherwise, merge the sets containing $v$ and $w$.
