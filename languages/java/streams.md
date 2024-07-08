# Streams

## Stream Pipeline

- **Stream Source**: Streams can be created from `Collections`, `Lists`, `int`s, `long`s, `double`s, arrays, lines of a file, etc.
- **Intermediate Operations**: Return a stream so we can chain together multiple of such operations. E.g. `map`, `filter`.
- **Terminal Operations**: Either `void` or return a non-stream result. E.g. `forEach`, `collect`, `reduce`.
