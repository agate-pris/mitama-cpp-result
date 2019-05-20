## and_then()

```cpp
template<class T, class E>
template<class O >
constexpr auto mitama::Result<T, E>::and_then(O && op) const &
```

Calls op if the result is Ok, otherwise returns the Err value of self.

This function can be used for control flow based on Result values.

**Condition**

```cpp
// for all type U:
std::invoke_result_t<O, T> => Result<U, E>
```

**Remarks**

This constructor shall not participate in overload resolution unless `is_result_with_v<std::invoke_result_t<O, T>, Err<E>>` is true.

**Example**

```cpp
auto sq = [](unsigned x) -> Result<unsigned, unsigned> { return Ok(x * x); };
auto err = [](unsigned x) -> Result<unsigned, unsigned> { return Err(x); };
assert_eq(Ok(2u).and_then(sq).and_then(sq), Ok(16u));
assert_eq(Ok(2u).and_then(sq).and_then(err), Err(4u));
assert_eq(Ok(2u).and_then(err).and_then(sq), Err(2u));
assert_eq(Err(3u).and_then(sq).and_then(sq), Err(3u));
```
