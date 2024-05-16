# Minimum Spanning Tree

- A *tree* is a collection of nodes connected by edges where there is exactly one path between any pair of nodes.
- A *spanning tree* is a tree that connects all the vertices in an undirected graph.
- The *minimum spanning tree* (MST) problem involves finding a spanning tree of minimum total weight in a connected and unweighted undirected graph.

## Problem Statement

- $G = (V, E)$ - An undirected graph with a set of vertices $V$ and edges $E$.
- $(u, v) \in E$ - Each edge of the graph from node $u$ to $v$.
- $w(u, v)$ - The weight of the edge from node $u$ to $v$.
- **Minimum Spanning Tree Problem**: Find an acyclic subset $T \sube E$ that connects all vertcies and whose total weight $w(T) = \sum_{(u,v) \in T}$ is minimized.

## Growing a Minimm Spanning Tree

- $A$ - Subset of some MST.

### Generic MST Algorithm

- While $A$ doesn't form a spanning tree, find an edge $(u, v)$ that is *safe* for $A$.
- Add the edge to A - $A = A \cup {(u, v)}$.

## Cycle Property

- Given any cycle, the heaviest edge must not be in the MST.

## Cut Property

- A *cut* of a graph is the separation of any nodes.
- A *crossing edge* is an edge that has one endpoint in each set of a cut.
- Given any cut, of all the edges crossing the cut, the one with the minimum weight must be in the MST.
