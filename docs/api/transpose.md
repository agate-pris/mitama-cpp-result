## transpose() [since 1.2.0]

```cpp
template < class T, class E >
auto mitama::Result<T, E>::transpose()
  -> std::optional<mitama::Result<T, E>>
```

Transposes a `Result` of an `optional` into an `optional` of a `Result`.

`Ok(nullopt)` will be mapped to `nullopt`.
`Ok(optional(v))` and `Err(v)` will be mapped to `optional(Ok(v))` and `optional(Err(v))`.

**Examples**

```cpp
struct SomeErr{};

Result<std::optional<int>, SomeErr> x = Ok(std::optional(5));
std::optional<Result<int, SomeErr>> y = std::optional(Result<int, SomeErr>(Ok(5)));
assert_eq!(x.transpose(), y);
```