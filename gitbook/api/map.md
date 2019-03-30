## map()

```cpp
template<class T, class E>
template<class O >
constexpr auto mitama::Result<T, E>::map(O && op)const & -> std::enable_if_t<std::is_invocable_v<O, T>, Result<std::invoke_result_t<O, T>, E>>
```

Maps a `Result<T, E>` to `Result<U, E>` by applying a function to a contained `Ok` value, leaving an `Err` value untouched.

This function can be used to compose the results of two functions.

**Example**

```cpp
std::string line = "1,3,5,7";
for (auto num : split(line, ","))
{
  if (auto res = parse<int>(num).map(_1 * 2); res.is_ok())
  {
    assert_true(res.ok().value() % 2 == 0);
  }
}
```
