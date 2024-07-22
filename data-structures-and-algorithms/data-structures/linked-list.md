# Linked List

## Overview

- A *linked list* is a data structure consisting of a series of linked nodes.
- Each node contains data and a pointer to the next / previous node (depending on whether the current implementation is a singly or doubly-linked list).

### Terminology

- **Node**: A single "unit" of the linked list, which is an object containing data and pointer(s).
- **Head**: The first node of the linked list.
- **Tail**: The last node of the linked list.
- **Pointer**: A reference to another node.

### Applications

- Backing data structure for stacks and queues.
- Great for creating circular lists.
- Can be used to model real-world objects.
- Used in separate chaining in hash table implementations.

### Singly vs Doubly Linked List

- **Singly-Linked List**: Each node contains a single pointer pointing to the next node.
- **Doubly-Linked List**: Each node contains two pointers, pointing to the previous and next nodes.

|        | Pros                                    | Cons                                      |
|--------|-----------------------------------------|-------------------------------------------|
| Singly | Less memory and simpler implementation  | Cannot easily access previous elements.   |
| Doubly | Can traverse backwards.                 | Takes 2x memory                           |

## Complexity Analysis

- **Search / Index - $O(N)$**: Because we don't have random access like arrays, we need to iterate through each node until we find the one we're searching for.
- **Insertion / Removal in Middle - $O(N)$**: We need to traverse to the middle of our linked-list which requires linear time. The remove operation is simply pointer manipulation which requires constant time.
- **Insertion / Removal at Head - $O(1)$**: Since we keep track of a pointer to the head of our list, we can apply our insertion / removal operation in constant time.
- **Insertion / Removal at Tail - $O(N)$ / $O(1)$** - Removal at the tail takes linear time for a singly-linked list as we need to traverse through the entire list. But for a doubly-linked list, we keep track of a pointer at the tail.

### Summary

| Method           | Singly-Linked | Doubly-Linked |
|------------------|:-------------:|:-------------:|
| Search / Index   |     $O(N)$    |     $O(N)$    |
| Insert at Head   |     $O(1)$    |     $O(1)$    |
| Insert at Tail   |     $O(N)$    |     $O(1)$    |
| Insert in Middle |     $O(N)$    |     $O(N)$    |
| Remove at Head   |     $O(1)$    |     $O(1)$    |
| Remove at Tail   |     $O(N)$    |     $O(1)$    |
| Remove in Middle |     $O(N)$    |     $O(N)$    |

## Linked-Lists vs Arrays
