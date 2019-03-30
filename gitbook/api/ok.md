## ok() [1/2]

```cpp
template<class T, class E>
constexpr std::optional<T> mitama::Result<T, E>::ok()const &
```

Converts from `Result<T, E>` to `std::optional<T>`.

Converts self into an `std::optional<T>`, copying self, and discarding the error, if any.

**Example**

```cpp
Result<unsigned, std::string> x = Ok(2);
assert_eq(x.err(), None);
Result<int, std::string> y = Err("Nothing here");
assert_eq(y.err(), Some("Nothing here"));
```

## ok() [2/2]

```cpp
template<class T, class E>
constexpr std::optional<T> mitama::Result<T, E>::ok()&&
```

Converts from `Result<T, E>` to `std::optional<T>`.

Converts self into an `std::optional<T>`, comsuming self, and discarding the error, if any.

