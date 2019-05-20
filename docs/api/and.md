## operator &&()

```cpp
template<class T, class E>
template<class U >
constexpr auto mitama::Result<T, E>::operator&&(Result< U, E > const & res)const & -> Result<U, E>
```

Returns res if the result is `Ok`, otherwise returns the `Err` value of self.

**Example**

```cpp
{
  Result<unsigned, std::string> x = Ok(2);
  Result<std::string, std::string> y = Err("late error"s);
  assert_eq(x && y, Err("late error"s));
}
{
  Result<unsigned, std::string> x = Err("early error"s);
  Result<std::string, std::string> y = Ok("foo"s);
  assert_eq(x && y, Err("early error"s));
}
{
  Result<unsigned, std::string> x = Err("not a 2"s);
  Result<std::string, std::string> y = Err("late error"s);
  assert_eq(x && y, Err("not a 2"s));
}
{
  Result<unsigned, std::string> x = Ok(2);
  Result<std::string, std::string> y = Ok("different result type"s);
  assert_eq(x && y, Ok("different result type"s));
}
```
