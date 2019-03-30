## err() [1/2]

```cpp
template<class T, class E>
constexpr std::optional<E> mitama::Result<T, E>::err()const &
```

Converts from `Result<T, E>` to `std::optional<E>`.

Converts self into an `std::optional<E>`, copying self, and discarding the success value, if any.

**Example**

```cpp
Result<unsigned, std::string> x = Ok(2);
assert_eq(x.err(), None);
Result<unsigned, std::string> y = Err("Nothing here");
assert_eq(y.err(), Some("Nothing here"));
```

## err() [2/2]

```cpp
template<class T, class E>
constexpr std::optional<E> mitama::Result<T, E>::err()&&
```

Converts from `Result<T, E>` to `std::optional<E>`.

Converts self into an `std::optional<E>`, consuming self, and discarding the success value, if any.

