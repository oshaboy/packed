# Packed

This is a simple header only C/C++ library that adds a more portable macro for defining a macro as being packed, since most compilers have different ways of defining it.

## How to use this library

```c
#include "packed.h"
// Or
#include <packed.h>

// Packed struct

PACKED_STRUCT(
    a {
        int a;
        char b;
        short c;
        int d;
    }
);

// Non-packed struct
struct b {
    int a;
    char b;
    short c;
    int d;
};

// On GCC, sizeof(struct a) == 11, and sizeof(struct b) == 12 (at the time of writing this)
```

This is the same for C++, however, you'd use `sizeof(a)` instead of `sizeof(struct a)`.

You only need to copy `packed.h` into your project, all other files aren't essential. (`main.c` and `main.cpp` are just used for testing).

This library is also compatible with the widely used `typedef struct x {} x;` pattern used in C, you just need to replace `struct x {}` in that example with `PACKED_STRUCT(x {})`.

## Compiler Support

These compilers are known to work:

- Clang (tested 14.0.6)
- GCC (tested 12.2.0)
- MSVC (tested v19.33)

If the compiler you use (idk, `icc`?) isn't listed on here then it currently isn't supported, however, feel free to submit a pull request updating `packed.h` to be able to support your compiler.

## Notes on PRs that add support for other compilers

- When a compiler does not support packed structs, then it's ok to create a PR that emits a warning message saying so (something along the lines of `This compiler does not support packed structs`), I'd prefer this over a message stating that a compiler is not supported.
- Any detection method that can't be done in C preprocessor code (ie. your compiler does not have any predefined macros) won't be accepted, this is to keep the time for `packed.h` to be compiled at a minimum.
