# Prim's Algorithm

- Start from the source node and choose the smallest edge to any of the neighbors not yet visited.
- Add the neighbor to the visited set.
- Repeat until all nodes are visited.

## Modified Prim's Algorithm

- If we want to find the minimum cost to connect all nodes, but not necessarily a MST, we can add a *super source node* which is connected to every other node and run Prim's algorithm from there.
