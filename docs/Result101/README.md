## class result

`result <T, E>` is a class template that  has success value type of `T` and failure value type of `E`.

Actually, it is a wrapper class of  `std::variant<success<T>, failure<E>>` that has a useful API.

