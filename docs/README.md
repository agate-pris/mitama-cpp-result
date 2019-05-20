# Introduction

Result is a header only C++17 library for error handling.


## Prerequisites and installation


| Compiler/Toolchain |                      Status                       |
| :----------------: | :-----------------------------------------------: |
|   clang >= 5.0.0   | Testing on Wandbox; tested on each push to GitHub |
|    gcc >= 7.1.0    | Testing on Wandbox; tested on each push to GitHub |

More specifically, Mitama.Result requires a compiler/standard library supporting the following C++17 features:

- constexpr if
- inline variables
- class template deduction and deduction guide
- All the C++17 type traits from the <type_traits> header
- std::optional from the <optional> header
- std::variant from the <variant> header


## Basic Usage

Here is a bad code, see below.

If this program fail to assert, you don't know the reason for the error.

```cpp
bool func(int a) {
  if ( first check )
    return false;
  if ( second check )
    return false;
  if ( third check )
    return false;
  // function body...
  return true;
}
// ...
assert(func(42));
```

Here is a code using Result.

Even if this program fail to assert, you can get the reason for the error.

```cpp
auto func(int a) -> mitama::Result<int, std::string> {
  if ( first check )
    return mitama::Err("first check failed"); // early return
  if ( second check )
    return mitama::Err("second check failed"); // early return
  if ( third check )
    return mitama::Err("third check failed"); // early return
  // function body...
  return mitama::Ok(42);
}
// ...
int value func(42).unwrap();
// even if fail to unwrap,
// raise runtime_panic
// and you get reason for the error.
```