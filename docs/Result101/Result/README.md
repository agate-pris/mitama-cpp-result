## class Result

`Result <T, E>` is a class template that  has Ok value type of `T` and Err value type of `E`.

Actually, it is a wrapper class of  `std::variant<Ok<T>, Err<E>>` that has a useful API.

