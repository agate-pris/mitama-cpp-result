## Deduction guide

```cpp
template <class T>
Ok(T &&)->Ok<std::decay_t<T>>;
```