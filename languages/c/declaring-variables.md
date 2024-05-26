# Declaring Variables

## Swapping Variables (Failed)

- The example below fails to permanently swap variables.

```c
void swap(int a, int b) {
    int t = a;
    a = b;
    b = t;
}
```

## Swapping Variables (Success)

- **Pointer**: A variable which *points* to an object in memory.
- **Indirection (`*`) Operator**: Used to *dereference* pointers. Dereferencing a pointer means that the pointer is no longer a reference - your variable points to the exact location in memory.
- **Address Of (&) Operator**: Used to get the memory address of a variable.

```c
void swap(int *pa, int *pb) {
    int t = *pa;
    *pa = *pb;
    *pb = t;
}

void main() {
    int a = 1;
    int b = 2;
    swap(&a, &b);
}
```
