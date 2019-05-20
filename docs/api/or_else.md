## or_else()

```cpp
template<class T, class E>
template<class O >
constexpr auto mitama::Result<T, E>::or_else(O && op)const &
```

Calls `op` if the result is `Err`, otherwise returns the `Ok` value of self.

This function can be used for control flow based on result values.

**Condition**

```cpp
// for all type F:
std::invoke_result_t<O, T> => Result<T, F>
```

**Remarks**

This constructor shall not participate in overload resolution unless `is_result_with_v<std::invoke_result_t<O, T>, Ok<T>>` is true.

**Example**

```cpp
auto sq = [](unsigned x) -> Result<unsigned, unsigned> { return Ok(x * x); };
auto err = [](unsigned x) -> Result<unsigned, unsigned> { return Err(x); };
assert_eq(Ok(2).or_else(sq).or_else(sq), Ok(2u));
assert_eq(Ok(2).or_else(err).or_else(sq), Ok(2u));
assert_eq(Err(3).or_else(sq).or_else(err), Ok(9u));
assert_eq(Err(3).or_else(err).or_else(err), Err(3u));
```
