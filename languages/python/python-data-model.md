# The Python Data Model

- Why do we call `len(array)` instead of `array.len()`?
- The *Python Data Model* centers around the use of magic/dunder methods in objects to provide a consistent API. For example, when we index an array, `array[1]`, we are calling the `__get__(1)` method of the array.
- This way, users can implement their own dunder methods for their objects and seamlessly integrate their code to work with the existing Python API.
