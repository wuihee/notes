# Dynamic Array

- A *dynamic array* is an array-like data structure that allows elements to be added and removed, and whose size can grow.
- The dynamic array relies on resizing an underlying array data structure to store elements.

## Complexity

| Method    | Complexity |
|-----------|:----------:|
| Access    |   $O(1)$   |
| Search    |   $O(N)$   |
| Insertion |   $O(N)$   |
| Appending |   $O(1)$   |
| Deletion  |   $O(N)$   |

## Amortized Cost

- When the number of elements in the dynamic array reaches the capacity of the underlying array, the dynamic array *resizes* and copies over its elements into a larger array (typically 2x in capacity).
