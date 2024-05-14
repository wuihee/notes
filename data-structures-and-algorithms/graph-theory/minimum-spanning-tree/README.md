# Minimum Spanning Tree

- A *tree* is a collection of nodes connected by edges where there is exactly one path between any pair of nodes.
- A *spanning tree* is a tree that connects all the vertices in an undirected graph.
- The *minimum spanning tree* (MST) problem involves finding a spanning tree of minimum total weight in a connected and unweighted undirected graph.

## Cycle Property

- Given any cycle, the heaviest edge must not be in the MST.

## Cut Property

- A *cut* of a graph is the separation of any nodes.
- A *crossing edge* is an edge that has one endpoint in each set of a cut.
- Given any cut, of all the edges crossing the cut, the one with the minimum weight must be in the MST.
