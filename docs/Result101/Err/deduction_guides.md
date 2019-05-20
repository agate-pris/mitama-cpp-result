## Deduction guide

```cpp
template <class T>
Err(T &&)->Err<std::decay_t<T>>;
```