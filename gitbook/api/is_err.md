## is_err()

```cpp
template<class T, class E>
constexpr bool mitama::Result<T, E>::is_err()const noexcept
```

Returns true if the result is Err.

**Example**

```cpp
Result<uint32_t, std::string> x = Ok(-3);
assert_eq(x.is_err(), false);
Result<uint32_t, std::string> y = Err("Some error message");
assert_eq(y.is_err(), true);
```
