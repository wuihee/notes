# Dijkstra's Algorithm

- *Dijkstra's algorithm* solves the single-source shortest-paths problem on a weighted, directed graph $G = (V, E)$, but it requires all nonnegative weights on all edges, where $w(u, v) \ge 0$ for each edge $(u, v) \in E$.
- Dijkstra's algorithm is like breadth-first search for weighted graphs, where we search layer-by-layer. However, each layer is determined by edge weights.
- Dijkstra maintains a set $S$ of vertices whose distances from the source have been determined. The algorithm repeatedly selects the vertex $u \in V - S$ with the minimum shortest path estimate, adds $u$ to $S$, and relaxes all edges leaving $u$. ($V - S$ is the set of all vertices in the graph whose distance from the source has not yet been found).
- Instead of using a queue like in breadth-first search, we use a priority queue $Q$.
