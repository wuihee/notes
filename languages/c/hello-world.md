# Hello World

- Basic hello world script:

    `helloworld.c`

    ```c
    #include<stdio.h>;
    #include<stdlib.h>;

    int main() {
        puts("Hello, World!");
        return EXIT_SUCCESS;
    }
    ```

## Compiling & Executing

- Compile. `-o` flag names the executable.

    ```bash
    cc -o helloworld helloworld.c
    ```

- Execute

    ```bash
    ./helloworld
    ```
