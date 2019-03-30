## operator||()

```cpp
template<class T, class E>
template<class F >
constexpr auto mitama::Result<T, E>::operator||(Result< T, F > const & res)const & -> Result<T, F>
```

Returns `res` if the result is `Err`, otherwise returns the `Ok` value of self.

Arguments passed to or are eagerly evaluated; if you are passing the result of a function call, it is recommended to use `or_else`, which is lazily evaluated.

**Example**

```cpp
{
  Result<unsigned, std::string> x = Ok(2);
  Result<unsigned, std::string> y = Err("late error"s);
  assert_eq(x || y, Ok(2u));
}
{
  Result<unsigned, std::string> x = Err("early error"s);
  Result<unsigned, std::string> y = Ok(2);
  assert_eq(x || y, Ok(2u));
}
{
  Result<unsigned, std::string> x = Err("not a 2"s);
  Result<unsigned, std::string> y = Err("late error"s);
  assert_eq(x || y, Err("late error"s));
}
{
  Result<unsigned, std::string> x = Ok(2);
  Result<unsigned, std::string> y = Ok(100);
  assert_eq(x || y, Ok(2u));
}
```

