# Storage Duration

- **Static Storage**: Objects declared in the file scope have static storage duration, which lasts the entire program.
- Using the `static` keyword can be used to give a variable defined in the block scope static storage, making them persist even after the function has exited.
- The example below outputs `1 2 3 4 5`. This is because the lifetime of `counter` is the entire duration of the file, so it retains its value even after `increment` finishes.

    ```c
    void increment(void) {
        static unsigned int counter = 0;
        counter++;
        printf("%d ", counter);
    }

    int main(void) {
        for (int i = 0; i < 5; i++) {
            increment();
        }
        return 0;
    }
    ```

- Static objects must be initialized with a constant value (`1`, `'a'`, etc.) and not a variable (`x`, `i`, etc).

    ```c
    int *func(int i) {
        const int j = i;   // Ok
        static int k = j;  // Error
        return &k;
    }
    ```

## Other Storage Types

- **Thread Storage**: Used in concurrent programming.
- **Allocated Storage**: Deals with dynamically allocated memory.

- What is `unsigned` and `const`.
