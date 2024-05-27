# Declaring Variables

## Address Of Operator (`&`)

- Retrieves the memory address of the variable.

    ```c
    int x = 1;

    // Prints the location in memory. E.g. 1777181520.
    printf("%d", &x);
    ```

## Indirection Operator (`*`)

1. **Pointer Declaration**: Indicates that a variable is a pointer.

    ```c
    int x = 1;
    int *px = &x;
    ```

2. **Dereferencing**: Access the value stored at that point in memory.

    ```c
    int x = 1;
    int *px = &x;

    // Prints the location in memory. E.g. 1992030900.
    printf("%d\n", px);  

    // Prints the value at `px`, which in this case is 1.
    printf("%d\n", *px);
    ```

## Example: Swapping Variables

- C *passes-by-reference*, meaning that when we pass our arguments into `swap1`, we are passing *references* of `a` and `b` which is why their values don't get swapped.

    ```c
    void swap1(int a, int b) {
        int t = a;
        a = b;
        b = t;
        printf("a: %d, b: %d\n", a, b);
        return;
    }

    int main() {
        int a = 1;
        int b = 2;
        swap1(a, b);                     // 2, 1
        printf("a: %d, b: %d\n", a, b);  // 1, 2
        return 0;
    }
    ```

- We use the *indirection operator* (*) to indicate that we are passing to `swap2` the memory locations of `a` and `b`, i.e the pointers `*pa` and `*pb`.
- In `swap2`, we change the values at the memory locations `*pa` and `*pb` by *dereferencing* them and swapping their values.
- In the `main` method, we use the *address of* (&) operator to indicate that we are passing in the memory addresses of `a` and `b` into `swap2`.

    ```c
    void swap2(int *pa, int *pb) {
        int t = *pa;
        *pa = *pb;
        *pb = t;
        printf("a: %d, b: %d\n", *pa, *pb);
        return;
    }

    int main() {
        int a = 1;
        int b = 2;
        swap2(&a, &b);                     // 2, 1
        printf("a: %d, b: %d\n", a, b);  // 2, 1
        return 0;
    }

    ```
