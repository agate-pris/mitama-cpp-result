## Err() [1/9]

```cpp
template<class T>
mitama::Err<T>::Err() = delete
```

default constructor is explicitly deleted.

## Err() [2/9]

```cpp
template<>
mitama::Err<std::monostate>::Err() = default
```

default constructor is explicitly defaulted.

## Err() [3/9]

```cpp
template<class T>
template<class U >
constexpr mitama::Err<T>::Err(U && u)
```

non-explicit generic constructor Initializes the contained variant as if direct-non-list-initializing an object of type `T` with the expression `std::forward<U>(u)`.

**Exceptions**

Any exception thrown by the selected constructor of `T`.

**Remarks**
The expression inside noexcept is equivalent to `is_nothrow_constructible_v<T, U>`. This constructor shall not participate in overload resolution unless `is_constructible_v<T, U> and is_conertible_v<U, T>` is true. If `is_trivially_constructible_v<T, U>` is true, this constructor shall be a constexpr constructor.

## Err() [4/9]

```cpp
template<class T>
template<class U >
explicit mitama::Err<T>::Err(U && u)
```

explicit generic constructor template Initializes the contained variant as if direct-non-list-initializing an object of type T with the expression `std::forward<U>(u)`.

**Exceptions**

Any exception thrown by the selected constructor of `T`.

**Remarks**

The expression inside noexcept is equivalent to `is_nothrow_constructible_v<T, U>`. This constructor shall not participate in overload resolution unless `is_constructible_v<T, U> and !is_conertible_v<U, T>` is true. If `is_trivially_constructible_v<T, U>` is true, this constructor shall be a constexpr constructor.

## Err() [5/9]

```cpp
template<class T>
template<typename U >
constexpr mitama::Err<T>::Err(const Err< U > & t)
```

non-explicit constructor for `Err` Initializes the contained variant as if direct-non-list-initializing an object of type `T` with the expression `t.x`.

**Exceptions**

Any exception thrown by the selected constructor of `T`.

**Remarks**

The expression inside noexcept is equivalent to `is_nothrow_constructible_v<T, U>`. This constructor shall not participate in overload resolution unless `is_constructible_v<T, U> and is_conertible_v<U, T>` is true. If `is_trivially_constructible_v<T, U>` is true, this constructor shall be a constexpr constructor.

## Err() [6/9]

```cpp
template<class T>
template<typename U >
explicit mitama::Err<T>::Err(const Err< U > & t)
```

explicit generic copy constructor Initializes the contained variant as if direct-non-list-initializing an object of type T with the expression `t.x`.

**Exceptions**

Any exception thrown by the selected constructor of `T`.

**Remarks**

The expression inside noexcept is equivalent to `is_nothrow_constructible_v<T, U>`. This constructor shall not participate in overload resolution unless `is_constructible_v<T, U> and !is_conertible_v<U, T>` is true. If `is_trivially_constructible_v<T, U>` is true, this constructor shall be a constexpr constructor.

## Err() [7/9]

```cpp
template<class T>
template<typename U >
constexpr mitama::Err<T>::Err(Err< U > && t)
```

non-explicit move constructor Initializes the contained variant as if direct-non-list-initializing an object of type `T` with the expression `t.x`.

**Exceptions**

Any exception thrown by the selected constructor of `T`.

**Remarks**

The expression inside noexcept is equivalent to `is_nothrow_constructible_v<T, U>`. This constructor shall not participate in overload resolution unless `is_constructible_v<T, U> and is_conertible_v<U, T>` is true. If `is_trivially_constructible_v<T, U>` is true, this constructor shall be a constexpr constructor.

## Err() [8/9]

```cpp
template<class T>
template<typename U >
constexpr mitama::Err<T>::Err(Err< U > && t)
```

explicit move constructor Initializes the contained variant as if direct-non-list-initializing an object of type `T` with the expression `t.x`.

**Exceptions**

Any exception thrown by the selected constructor of `T`.

**Remarks**

The expression inside noexcept is equivalent to `is_nothrow_constructible_v<T, U>`. This constructor shall not participate in overload resolution unless `is_constructible_v<T, U> and !is_conertible_v<U, T>` is true. If `is_trivially_constructible_v<T, U>` is true, this constructor shall be a constexpr constructor.

## Err() [9/9]

```cpp
template<class T>
template<class... Args>
constexpr mitama::Err<T>::Err(std::in_place_t, Args &&... args)

in-place constructor Initializes the contained variant as if direct-non-list-initializing an object of type `T` with the expression `std::forward<Args>(args)...`.

**Exceptions**

Any exception thrown by the selected constructor of `T`.

**Remarks**

The expression inside noexcept is equivalent to `is_nothrow_constructible_v<T, U>`. This constructor shall not participate in overload resolution unless `is_constructible_v<T, U> and !is_conertible_v<U, T>` is true. If `is_trivially_constructible_v<T, U>` is true, this constructor shall be a constexpr constructor.