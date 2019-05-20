## class Err

`Err` is a helper class to construct `Result`.
`Result` has constructor 

**Example**

```cpp
#include <string>
[](auto value) -> Result<int, std::string> {
    using namespace std::literals;
    if (value)
        return Ok(value);
    else
        return Err("error"s);
};
```