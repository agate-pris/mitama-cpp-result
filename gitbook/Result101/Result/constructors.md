# Constructors


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
