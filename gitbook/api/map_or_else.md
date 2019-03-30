## map_or_else() [since 1.2.0]

```cpp
template <class Map, class Fallback, class U = T, class F = E>
constexpr auto map_or_else(Fallback&& _fallback, Map&& _map) const&
    -> std::common_type_t<std::invoke_result_t<Map, T>, std::invoke_result_t<Fallback, E>>
``` 

Maps a `Result<T, E>` to `U` by applying a function to a contained `Ok` value, or a fallback function to a contained `Err` value.

This function can be used to unpack a successful result while handling an error.

**Examples**

Basic usage:

```cpp
auto k = 21;
{
    Result<std::string, std::string> x = Ok("foo"s);
    assert(x.map_or_else([k](auto){ return k * 2; }, [](auto v) { return v.length(); }) == 3);
}
{
    Result<std::string, std::string> x = Err("bar"s);
    assert(x.map_or_else([k](auto){ return k * 2; }, [](auto v) { return v.length(); }) == 42);
}
```