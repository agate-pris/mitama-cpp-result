## map_err()

```cpp
template<class T, class E>
template<class O >
constexpr auto mitama::Result<T, E>::map_err(O && op)const & -> std::enable_if_t<std::is_invocable_v<O, E>, Result<T, std::invoke_result_t<O, E>>>
```

Maps a `Result<T, E>` to `Result<T, F>` by applying a function to a contained Err value, leaving an Ok value untouched.

This function can be used to pass through a successful result while handling an error.

**Example**

```cpp
auto stringify = [](unsigned x) -> std::string{
  return "error code: "s + std::to_string(x);
};
Result<unsigned, unsigned> x = Ok(2);
assert_eq(x.map_err(stringify), Ok(2u));
Result<unsigned, unsigned> y = Err(13);
assert_eq(y.map_err(stringify), Err("error code: 13"s));
```
