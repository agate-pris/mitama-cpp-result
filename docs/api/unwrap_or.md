## unwrap_or()

```cpp
template<class T, class E>
T mitama::Result<T, E>::unwrap_or(T const & optb) const noexcept
```

Unwraps a result, yielding the content of an `Ok`. Else, it returns `optb`.

Arguments passed to unwrap_or are eagerly evaluated; if you are passing the result of a function call, it is recommended to use `unwrap_or_else`, which is lazily evaluated.

**Example**

```cpp
Result<unsigned, unsigned> err = Err(2);
Result<unsigned, unsigned> ok = Ok(2);
assert_eq(ok.unwrap_or(1u), 2u);
assert_eq(err.unwrap_or(1u), 1u);
```
