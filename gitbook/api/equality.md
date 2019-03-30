## operator==() [1/3]

```cpp
template<class T, class E>
template<class U , class F >
bool mitama::Result<T, E>::operator==(Result< U, F > const & rhs)const &
```

Operator== for `Result<T, E>` and `Result<U, F>`.

**Remarks**

This operator shall be defined as deleted unless `std::declval<T const&>() == std::declval<U const&>()` is valid expression and `std::declval<E const&>() == std::declval<F const&>()` is valid expression.

## operator==() [2/3]

```cpp
template<class T, class E>
template<class U >
bool mitama::Result<T, E>::operator==(Ok< U > const & rhs)const
```

Operator== for `Result<T, E>` and `Ok<U>`.

**Returns**

true if this has `Ok` value `this->unwrap()` equals `rhs` value, otherwise `false`.

**Remarks**

This operator shall be defined as deleted unless `std::declval<T const&>() == std::declval<U const&>()` is valid expression.


## operator==() [3/3]

```cpp
template<class T, class E>
template<class F >
bool mitama::Result<T, E>::operator==(Err< F > const & rhs)const
```

Operator== for `Result<T, E>` and `Err<F>`.

**Returns**

`true` if this has `Err` value `this->unwrap_err()` equals `rhs` value, otherwise `false`.

**Remarks**

This operator shall be defined as deleted unless `std::declval<E const&>() == std::declval<F const&>()` is valid expression.

