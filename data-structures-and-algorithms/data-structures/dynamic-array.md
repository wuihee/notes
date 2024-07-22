# Dynamic Array

## Overview

- A *dynamic array* is an array-like data structure that allows elements to be added and removed, and whose size can grow.
- The dynamic array relies on resizing an underlying array data structure to store elements.

## Complexity Analysis

- **Access - $O(1)$**: Accessing elements in a dynamic array is fast, because it has *random access* as we are actually accessing an array by index.
- **Search - $O(N)$**: To search for an element, we need to iterate through the entire underlying array.
- **Insertion - $O(N)$**: To insert in the middle, we need to shift over all elements to the right which in the worst case has linear time complexity.
- **Appending - $O(1)$**: Adding to the end of an array takes constant time. Despite occasionally requiring resizing, the *amortized cost* is still constant.
- **Deletion - $O(N)$**: Like insertion, deleting an element requires all elements to be shifted to the left. In the worst case, this also takes linear time.

### Summary

| Method    | Complexity |
|-----------|:----------:|
| Access    |   $O(1)$   |
| Search    |   $O(N)$   |
| Insertion |   $O(N)$   |
| Appending |   $O(1)$   |
| Deletion  |   $O(N)$   |

## Amortized Cost

- When the number of elements in the dynamic array reaches the capacity of the underlying array, the dynamic array *resizes* and copies over its elements into a larger array (typically 2x in capacity).
