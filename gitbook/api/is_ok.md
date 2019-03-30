## is_ok()

```cpp
template<class T, class E>
constexpr bool mitama::Result<T, E>::is_ok()const noexcept
```

Returns true if the result is `Ok`.

**Example**

```cpp
Result<uint32_t, std::string> x = Ok(-3);
assert(x.is_ok(), true);
Result<uint32_t, std::string> y = Err("Some error message");
assert(y.is_ok(), false);
```
