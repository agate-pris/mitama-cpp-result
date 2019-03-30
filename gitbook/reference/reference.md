# Result user reference

## Result(Result const&) [1/14]

```cpp
template<class T, class E>
constexpr mitama::Result<T, E>::Result(const Result<T, E>& rhs)
```

Copy constructor. Initializes the contained variant as.

**Exceptions**

Any exception thrown by the selected constructor of `T` or `E`.

**Remarks**

This constructor shall be defined as deleted unless `is_copy_constructible_v<T> && is_copy_constructible_v<E>` is true.

If `is_trivially_copy_constructible_v<T> && is_trivially_copy_constructible_v<E>` is true, this constructor shall be a constexpr constructor.

## Result(Result&&) [2/14]

```cpp
template<class T, class E>
constexpr mitama::Result<T, E>::Result(Result<T, E> && rhs)
```
Move constructor. Initializes the contained variant.

**Exceptions**

Any exception thrown by the selected constructor of `T` or `E`.

**Remarks**

The expression inside noexcept is equivalent to `is_nothrow_move_constructible_v<T> && is_nothrow_move_constructible_v<E>`.

This constructor shall not participate in overload resolution unless `is_move_constructible_v<T> && is_move_constructible_v<E>` is true.

If `is_trivially_move_constructible_v<T> && is_trivially_move_constructible_v<T>` is true, this constructor shall be a constexpr constructor.

## Result() [3/14]

```cpp
template<class T, class E>
template<class U >
mitama::Result<T, E>::Result(Ok<U> const& ok)
```

constructor from `Ok const&`.

Initializes the contained variant as if in-place-initializing an object of type `Ok<T> const&`.

**Exceptions**

Any exception thrown by the selected constructor of T.

**Remarks**

This constructor shall not participate in overload resolution unless `is_constructible_v<T, U> && is_convertible_v<U, T>` is true.

## Result() [4/14]

```cpp
template<class T, class E>
template<class U >
explicit mitama::Result<T, E>::Result(Ok<U> const& ok)
```

constructor for `Ok const&`

Initializes the contained variant as if in-place-initializing an object of type Ok<T> const&.

**Exceptions**

Any exception thrown by the selected constructor of `T`.

**Remarks**

This constructor shall not participate in overload resolution unless `is_constructible_v<T, U> && !is_convertible_v<U, T>` is true.


## Result() [5/14]

```cpp
template<class T, class E>
template<class U >
mitama::Result<T, E>::Result(Ok<U>&& ok)
```

constructor for `Ok&&`.

Initializes the contained variant as if in-place-initializing an object of type `Ok<T>&&`.

**Exceptions**

Any exception thrown by the selected constructor of T.

**Remarks**

This constructor shall not participate in overload resolution unless `is_constructible_v<T, U> && is_convertible_v<U, T>` is true.

## Result() [6/14]

```cpp
template<class T, class E>
template<class U >
explicit mitama::Result<T, E>::Result(Ok< U > && ok)
```

constructor for `Ok&&`.

Initializes the contained variant as if in-place-initializing an object of type `Ok<T>&&`.

**Exceptions**

Any exception thrown by the selected constructor of T.

**Remarks**

This constructor shall not participate in overload resolution unless `is_constructible_v<T, U> && !is_convertible_v<U, T>` is true.

## Result() [7/14]

```cpp
template<class T, class E>
template<class U >
mitama::Result<T, E>::Result(Err< U > const & err)
```

constructor for `Err const&`.

Initializes the contained variant as if in-place-initializing an object of type `Err<E> const&`.

**Exceptions**

Any exception thrown by the selected constructor of `E`.

**Remarks**

This constructor shall not participate in overload resolution unless `is_constructible_v<E, U> && is_convertible_v<U, E>` is true.

## Result() [8/14]

```cpp
template<class T, class E>
template<class U >
explicit mitama::Result<T, E>::Result(Err< U > const & err)
```

constructor for `Err const&`.

Initializes the contained variant as if in-place-initializing an object of type `Err<E> const&`.

**Exceptions**

Any exception thrown by the selected constructor of `E`.

**Remarks**

This constructor shall not participate in overload resolution unless `is_constructible_v<E, U> && !is_convertible_v<U, E>` is true.

## Result() [9/14]

```cpp
template<class T, class E>
template<class U >
mitama::Result<T, E>::Result(Err< U > && err)
```

constructor for `Err&&`.

Initializes the contained variant as if in-place-initializing an object of type `Err<E>&&`.

**Exceptions**

Any exception thrown by the selected constructor of E.

**Remarks**

This constructor shall not participate in overload resolution unless `is_constructible_v<E, U> && is_convertible_v<U, E>` is true.

## Result() [10/14]

```cpp
template<class T, class E>
template<class U >
explicit mitama::Result<T, E>::Result(Err< U > && err)
```

constructor for `Err&&`.

Initializes the contained variant as if in-place-initializing an object of type `Err<E>&&`.

**Exceptions**
Any exception thrown by the selected constructor of `E`.

**Remarks**

This constructor shall not participate in overload resolution unless `is_constructible_v<E, U> && !is_convertible_v<U, E>` is true.

## Result() [11/14]

```cpp
template<class T, class E>
template<class... Args>
explicit mitama::Result<T, E>::Result(in_place_ok_t, Args &&... args)
```
constructor for ok value.

Initializes the contained variant as if in-place-initializing an object of type with expression `(std::in_place_type<Ok<T>>, std::forward<Args>(args)...)`.

**Exceptions**

Any exception thrown by the selected constructor of `T`.

**Example**

```cpp
using my_result = Result<std::tuple<int, int>, std::string>;
auto res = my_result( mitama::in_place_ok, 1, 1 );
// same as `my_result(Ok(std::tuple{1,1}))`
```

## Result() [12/14]

```cpp
template<class T, class E>
template<class... Args>
explicit mitama::Result<T, E>::Result(in_place_err_t, Args&&... args)
```

constructor for ok value

Initializes the contained variant as if in-place-initializing an object of type with expression `(std::in_place_type<Err<E>>, std::forward<Args>(args)...)`.

**Exceptions**

Any exception thrown by the selected constructor of `E`.

**Example**

```cpp
using my_result = Result<int, std::string>;
auto res = my_result( mitama::in_place_err, 'a', 5 ); // Err("aaaaa")
```

## Result() [13/14]

```cpp
template<class T, class E>
template<class U , class... Args>
explicit mitama::Result<T, E>::Result(in_place_ok_t, 
                                      std::initializer_list< U > il,
                                      Args &&... args)
```

constructor for ok value.

Initializes the contained variant as if in-place-initializing an object of type with expression `(std::in_place_type<Ok<T>>, il, std::forward<Args>(args)...)`.

**Exceptions**

Any exception thrown by the selected constructor of T.

**Example**

```cpp
using my_result = Result<std::vector<int>, std::string>;
auto res = my_result( mitama::in_place_ok, {1,2,3,4}, std::allocator<int>()); // Ok([1,2,3,4])
```

## Result() [14/14]

```cpp
template<class T, class E>
template<class U , class... Args>
explicit mitama::Result<T, E>::Result(in_place_ok_t ,
                                      std::initializer_list< U > il,
                                      Args&&... args)
```

constructor for err value.

Initializes the contained variant as if in-place-initializing an object of type with expression `(std::in_place_type<Err<E>>, il, std::forward<Args>(args)...)`.

**Exceptions**

Any exception thrown by the selected constructor of `E`.

**Example**

```cpp
using my_result = Result<std::string, std::vector<int>>;
auto res = my_result( mitama::in_place_err, {1,2,3,4}); // Err([1,2,3,4])
```

# Member Function Documentation

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

This constructor shall not participate in overload resolution unless `is_result_v<std::invoke_result_t<O, T>>` is true.

**Example**

auto sq = [](unsigned x) -> Result<unsigned, unsigned> { return Ok(x * x); };
auto err = [](unsigned x) -> Result<unsigned, unsigned> { return Err(x); };
assert_eq(Ok(2u).and_then(sq).and_then(sq), Ok(16u));
assert_eq(Ok(2u).and_then(sq).and_then(err), Err(4u));
assert_eq(Ok(2u).and_then(err).and_then(sq), Err(2u));
assert_eq(Err(3u).and_then(sq).and_then(sq), Err(3u));
## err() [1/2]
template<class T, class E>
constexpr std::optional<E> mitama::Result<T, E>::err()const &
inline
Converts from Result<T, E> to std::optional<E>.

Converts self into an std::optional<E>, copying self, and discarding the success value, if any.

Example
Result<unsigned, std::string> x = Ok(2);
assert_eq(x.err(), None);
Result<unsigned, std::string> y = Err("Nothing here");
assert_eq(y.err(), Some("Nothing here"));
## err() [2/2]
template<class T, class E>
constexpr std::optional<E> mitama::Result<T, E>::err()&&
inline
Converts from Result<T, E> to std::optional<E>.

Converts self into an std::optional<E>, consuming self, and discarding the success value, if any.

## is_err()
template<class T, class E>
constexpr bool mitama::Result<T, E>::is_err()const
inlinenoexcept
Returns true if the result is Err.

Example
Result<uint32_t, std::string> x = Ok(-3);
assert(x.is_err(), false);
Result<uint32_t, std::string> y = Err("Some error message");
assert_(y.is_err(), true);
## is_ok()
template<class T, class E>
constexpr bool mitama::Result<T, E>::is_ok()const
inlinenoexcept
Returns true if the result is Ok.

Example
Result<uint32_t, std::string> x = Ok(-3);
assert(x.is_ok(), true);
Result<uint32_t, std::string> y = Err("Some error message");
assert(y.is_ok(), false);
## map()
template<class T, class E>
template<class O >
constexpr auto mitama::Result<T, E>::map(O && op)const & -> std::enable_if_t<std::is_invocable_v<O, T>, Result<std::invoke_result_t<O, T>, E>>
inline
Maps a Result<T, E> to Result<U, E> by applying a function to a contained Ok value, leaving an Err value untouched.

This function can be used to compose the results of two functions.

Example
std::string line = "1,3,5,7";
for (auto num : split(line, ","))
{
  if (auto res = parse<int>(num).map(_1 * 2); res.is_ok())
  {
    assert_true(res.ok().value() % 2 == 0);
  }
}
## map_err()
template<class T, class E>
template<class O >
constexpr auto mitama::Result<T, E>::map_err(O && op)const & -> std::enable_if_t<std::is_invocable_v<O, E>, Result<T, std::invoke_result_t<O, E>>>
inline
Maps a Result<T, E> to Result<T, F> by applying a function to a contained Err value, leaving an Ok value untouched.

This function can be used to pass through a successful result while handling an error.

Example
auto stringify = [](unsigned x) -> std::string{
  return "error code: "s + std::to_string(x);
};
Result<unsigned, unsigned> x = Ok(2);
assert_eq(x.map_err(stringify), Ok(2u));
Result<unsigned, unsigned> y = Err(13);
assert_eq(y.map_err(stringify), Err("error code: 13"s));
## ok() [1/2]
template<class T, class E>
constexpr std::optional<T> mitama::Result<T, E>::ok()const &
inline
Converts from Result<T, E> to std::optional<T>.

Converts self into an std::optional<T>, copying self, and discarding the error, if any.

Example
Result<unsigned, std::string> x = Ok(2);
assert_eq(x.err(), None);
Result<int, std::string> y = Err("Nothing here");
assert_eq(y.err(), Some("Nothing here"));
## ok() [2/2]
template<class T, class E>
constexpr std::optional<T> mitama::Result<T, E>::ok()&&
inline
Converts from Result<T, E> to std::optional<T>.

Converts self into an std::optional<T>, comsuming self, and discarding the error, if any.

## operator &&()
template<class T, class E>
template<class U >
constexpr auto mitama::Result<T, E>::operator&&(Result< U, E > const & res)const & -> Result<U, E>
inline
Returns res if the result is Ok, otherwise returns the Err value of self.

Example
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
## operator==() [1/3]
template<class T, class E>
template<class U , class F >
bool mitama::Result<T, E>::operator==(Result< U, F > const & rhs)const &
inline
Operator== for Result<T, E> and Result<U, F>.

Remarks
This operator shall be defined as deleted unless std::declval<T const&>() == std::declval<U const&>() is valid expression and std::declval<E const&>() == std::declval<F const&>() is valid expression.
## operator==() [2/3]
template<class T, class E>
template<class U >
bool mitama::Result<T, E>::operator==(Ok< U > const & rhs)const
inline
Operator== for Result and Ok.

Returns
true if this has Ok value this->unwrap() equals rhs value, otherwise false.
Remarks
This operator shall be defined as deleted unless std::declval<T const&>() == std::declval<U const&>() is valid expression.
## operator==() [3/3]
template<class T, class E>
template<class F >
bool mitama::Result<T, E>::operator==(Err< F > const & rhs)const
inline
Operator== for Result<T, E> and Err<F>.

Returns
true if this has Err value this->unwrap_err() equals rhs value, otherwise false.
Remarks
This operator shall be defined as deleted unless std::declval<E const&>() == std::declval<F const&>() is valid expression.
## operator||()
template<class T, class E>
template<class F >
constexpr auto mitama::Result<T, E>::operator||(Result< T, F > const & res)const & -> Result<T, F>
inline
Returns res if the result is Err, otherwise returns the Ok value of self.

Arguments passed to or are eagerly evaluated; if you are passing the result of a function call, it is recommended to use or_else, which is lazily evaluated.

Example
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
## or_else()
template<class T, class E>
template<class O >
constexpr auto mitama::Result<T, E>::or_else(O && op)const & -> std::enable_if_t<is_result_v<std::invoke_result_t<O, E>>, std::invoke_result_t<O, E>>
inline
Calls op if the result is Err, otherwise returns the Ok value of self.

This function can be used for control flow based on result values.

Remarks
This constructor shall not participate in overload resolution unless is_result_v<std::invoke_result_t<O, T>> is true.
Example
auto sq = [](unsigned x) -> Result<unsigned, unsigned> { return Ok(x * x); };
auto err = [](unsigned x) -> Result<unsigned, unsigned> { return Err(x); };
assert_eq(Ok(2).or_else(sq).or_else(sq), Ok(2u));
assert_eq(Ok(2).or_else(err).or_else(sq), Ok(2u));
assert_eq(Err(3).or_else(sq).or_else(err), Ok(9u));
assert_eq(Err(3).or_else(err).or_else(err), Err(3u));
## unwrap()
template<class T, class E>
T mitama::Result<T, E>::unwrap()const
inline
Unwraps a result, yielding the content of an Ok.

Example
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
## unwrap_err()
template<class T, class E>
E mitama::Result<T, E>::unwrap_err()const
inline
Unwraps a result, yielding the content of an Err.

Example
try {
  Result<unsigned, std::string> x = Ok(2);
  x.unwrap_err(); // panics with `2`
}
catch (runtime_panic const &panic)
{
   std::err << panic.what() << std::endl; // 2
}
{
  Result<unsigned, std::string> x = Err("emergency failure"s);
  assert_eq(x.unwrap_err(), "emergency failure"s);
}
## unwrap_or()
template<class T, class E>
T mitama::Result<T, E>::unwrap_or(T const & optb)const
inlinenoexcept
Unwraps a result, yielding the content of an Ok. Else, it returns optb.

Arguments passed to unwrap_or are eagerly evaluated; if you are passing the result of a function call, it is recommended to use unwrap_or_else, which is lazily evaluated.

Example
Result<unsigned, unsigned> err = Err(2);
Result<unsigned, unsigned> ok = Ok(2);
assert_eq(ok.unwrap_or(1u), 2u);
assert_eq(err.unwrap_or(1u), 1u);
## unwrap_or_default()
template<class T, class E>
T mitama::Result<T, E>::unwrap_or_default()const &
inline
Returns the contained value or a default.

If Ok, returns the contained value, otherwise if Err, returns the default value for that type.

Remarks
This operator shall be defined as deleted unless is_default_constructible_v<T> is true.
Example
auto good_year_from_input = "1909"s;
auto bad_year_from_input = "190blarg"s;
auto good_year = parse<int>(good_year_from_input).unwrap_or_default();
auto bad_year = parse<int>(bad_year_from_input).unwrap_or_default();
assert_eq(1909, good_year);
assert_eq(0, bad_year);   * 
## unwrap_or_else()
template<class T, class E>
template<class O >
auto mitama::Result<T, E>::unwrap_or_else(O && op)const -> std::enable_if_t<std::is_invocable_r_v<T, O, E>, T>
inlinenoexcept
Unwraps a result, yielding the content of an Ok. If the value is an Err then it calls op with its value.

Example
auto count = [](std::stringx) -> size_t { return x.size(); };
assert_eq(Ok(2).unwrap_or_else(count), 2);
assert_eq(Err("foo"s).unwrap_or_else(count), 3);
The documentation for this class was generated from the following file:
Result.hpp
