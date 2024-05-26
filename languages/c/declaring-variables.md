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
