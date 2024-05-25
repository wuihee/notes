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
