# One-Hot Encoding

- We can use *one-hot encoding* to encode features with more than two values.
- This is useful for representing our features in a way that our machine learning models will understand.
- E.g. if we have a feature "ear shape" with 3 categories:

    | Ear Shape |
    |-----------|
    | Pointy    |
    | Round     |
    | Flat      |

- We can use one-hot encoding to represent them as 3 separate features.

    | Pointy | Round | Flat |
    |--------|-------|------|
    | 1      | 0     | 0    |
    | 0      | 1     | 0    |
    | 0      | 0     | 1    |
