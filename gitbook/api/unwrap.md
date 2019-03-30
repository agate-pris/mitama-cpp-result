## unwrap()

```cpp
template<class T, class E>
T mitama::Result<T, E>::unwrap()const
```

Unwraps a result, yielding the content of an `Ok`.

**Exception**

Raise `mitama::runtime_panic` if a result is containing `Err` value.

**Example**

```cpp
{
  Result<unsigned, std::string> x = Ok(2);
  assert_eq(x.unwrap(), 2);
}
try {
  Result<unsigned, std::string> x = Err("emergency failure"s);
  x.unwrap(); // panics with `emergency failure`
}
catch ( mitama::runtime_panic cosnt & panic ) {
  std::err << panic.what() << std::endl; // `emergency failure`
}
```
