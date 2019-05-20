## Ok() [1/9]

```cpp
template<class T>
mitama::Ok<T>::Ok() = delete
```

default constructor is explicitly deleted.

## Ok() [2/9]

```cpp
template<>
mitama::Ok<std::monostate>::Ok() = default
```

default constructor is explicitly defaulted.

## Ok() [3/9]

```cpp
template<class T>
template<class U >
constexpr mitama::Ok<T>::Ok(U && u)
```

non-explicit generic constructor Initializes the contained variant as if direct-non-list-initializing an object of type `T` with the expression `std::forward<U>(u)`.

**Exceptions**

Any exception thrown by the selected constructor of `T`.

**Remarks**
The expression inside noexcept is equivalent to `is_nothrow_constructible_v<T, U>`. This constructor shall not participate in overload resolution unless `is_constructible_v<T, U> and is_conertible_v<U, T>` is true. If `is_trivially_constructible_v<T, U>` is true, this constructor shall be a constexpr constructor.

## Ok() [4/9]

```cpp
template<class T>
template<class U >
explicit mitama::Ok<T>::Ok(U && u)
```

explicit generic constructor template Initializes the contained variant as if direct-non-list-initializing an object of type T with the expression `std::forward<U>(u)`.

**Exceptions**

Any exception thrown by the selected constructor of `T`.

**Remarks**

The expression inside noexcept is equivalent to `is_nothrow_constructible_v<T, U>`. This constructor shall not participate in overload resolution unless `is_constructible_v<T, U> and !is_conertible_v<U, T>` is true. If `is_trivially_constructible_v<T, U>` is true, this constructor shall be a constexpr constructor.

## Ok() [5/9]

```cpp
template<class T>
template<typename U >
constexpr mitama::Ok<T>::Ok(const Ok< U > & t)
```

non-explicit constructor for `Ok` Initializes the contained variant as if direct-non-list-initializing an object of type `T` with the expression `t.x`.

**Exceptions**

Any exception thrown by the selected constructor of `T`.

**Remarks**

The expression inside noexcept is equivalent to `is_nothrow_constructible_v<T, U>`. This constructor shall not participate in overload resolution unless `is_constructible_v<T, U> and is_conertible_v<U, T>` is true. If `is_trivially_constructible_v<T, U>` is true, this constructor shall be a constexpr constructor.

## Ok() [6/9]

```cpp
template<class T>
template<typename U >
explicit mitama::Ok<T>::Ok(const Ok< U > & t)
```

explicit generic copy constructor Initializes the contained variant as if direct-non-list-initializing an object of type T with the expression `t.x`.

**Exceptions**

Any exception thrown by the selected constructor of `T`.

**Remarks**

The expression inside noexcept is equivalent to `is_nothrow_constructible_v<T, U>`. This constructor shall not participate in overload resolution unless `is_constructible_v<T, U> and !is_conertible_v<U, T>` is true. If `is_trivially_constructible_v<T, U>` is true, this constructor shall be a constexpr constructor.

## Ok() [7/9]

```cpp
template<class T>
template<typename U >
constexpr mitama::Ok<T>::Ok(Ok< U > && t)
```

non-explicit move constructor Initializes the contained variant as if direct-non-list-initializing an object of type `T` with the expression `t.x`.

**Exceptions**

Any exception thrown by the selected constructor of `T`.

**Remarks**

The expression inside noexcept is equivalent to `is_nothrow_constructible_v<T, U>`. This constructor shall not participate in overload resolution unless `is_constructible_v<T, U> and is_conertible_v<U, T>` is true. If `is_trivially_constructible_v<T, U>` is true, this constructor shall be a constexpr constructor.

## Ok() [8/9]

```cpp
template<class T>
template<typename U >
constexpr mitama::Ok<T>::Ok(Ok< U > && t)
```

explicit move constructor Initializes the contained variant as if direct-non-list-initializing an object of type `T` with the expression `t.x`.

**Exceptions**

Any exception thrown by the selected constructor of `T`.

**Remarks**

The expression inside noexcept is equivalent to `is_nothrow_constructible_v<T, U>`. This constructor shall not participate in overload resolution unless `is_constructible_v<T, U> and !is_conertible_v<U, T>` is true. If `is_trivially_constructible_v<T, U>` is true, this constructor shall be a constexpr constructor.

## Ok() [9/9]

```cpp
template<class T>
template<class... Args>
constexpr mitama::Ok<T>::Ok(std::in_place_t, Args &&... args)

in-place constructor Initializes the contained variant as if direct-non-list-initializing an object of type `T` with the expression `std::forward<Args>(args)...`.

**Exceptions**

Any exception thrown by the selected constructor of `T`.

**Remarks**

The expression inside noexcept is equivalent to `is_nothrow_constructible_v<T, U>`. This constructor shall not participate in overload resolution unless `is_constructible_v<T, U> and !is_conertible_v<U, T>` is true. If `is_trivially_constructible_v<T, U>` is true, this constructor shall be a constexpr constructor.