## unwrap_or_else()

```cpp
template<class T, class E>
template<class O >
auto mitama::Result<T, E>::unwrap_or_else(O && op) const noexcept -> std::enable_if_t<std::is_invocable_r_v<T, O, E>, T>
```

Unwraps a result, yielding the content of an `Ok`. If the value is an `Err` then it calls `op` with its value.

**Example**

```cpp
auto count = [](std::stringx) -> size_t { return x.size(); };
assert_eq(Ok(2).unwrap_or_else(count), 2);
assert_eq(Err("foo"s).unwrap_or_else(count), 3);
```

