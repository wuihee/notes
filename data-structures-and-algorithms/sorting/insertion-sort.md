# Insertion Sort

## Intuition

- Moving through an unsorted array, we take each element and *insert* it in its correct position.
- To do this, we move the current element back along the array until the element behind it is less or equal.

## Code

```python
def insertion_sort(array):
    for i in range(1, len(array)):
        key = array[i]
        j = i - 1

        while j >= 0 and array[j] < key:
            array[j + 1] = array[j]

        array[j + 1] = key
```

## Complexity Analysis

- **Time Complexity**: $O(N^2)$
- **Space Complexity**: $O(1)$

## Proof of Correctness

- **Loop Invariant**: At the start of each iteration of the for loop, subarray `A[:i]` is in sorted order.
- **Initialization**: At the start, the subarray only contains a single element so it is already sorted.
- **Maintenance**: At each iteration, we move the current element to the left until it is in its correct place. Therefore, incrementing $i$ preserves the loop invariant that `A[:i]` is sorted.
- **Termination**: The loop terminates when $i = n$. If we substitute this into our loop invariant, we can see that the entire array `A[:n]` is sorted.
