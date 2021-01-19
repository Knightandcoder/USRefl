```

 __    __       _______..______       _______  _______  __      
|  |  |  |     /       ||   _  \     |   ____||   ____||  |     
|  |  |  |    |   (----`|  |_)  |    |  |__   |  |__   |  |     
|  |  |  |     \   \    |      /     |   __|  |   __|  |  |     
|  `--'  | .----)   |   |  |\  \----.|  |____ |  |     |  `----.
 \______/  |_______/    | _| `._____||_______||__|     |_______|
                                                                

```

[![repo-size](https://img.shields.io/github/languages/code-size/Ubpa/USRefl?style=flat)](https://github.com/Ubpa/USRefl/archive/master.zip) [![tag](https://img.shields.io/github/v/tag/Ubpa/USRefl)](https://github.com/Ubpa/USRefl/tags) [![license](https://img.shields.io/github/license/Ubpa/USRefl)](LICENSE) [![compiler explorer](https://img.shields.io/badge/compiler_explorer-online-blue)](https://godbolt.org/z/h4zWEM) 

⭐ Star us on GitHub — it helps!

# USRefl

> **U**bpa **S**tatic **R**eflection

Header-only, tiny (99 lines) and powerful C++20 static reflection library.

## Feature

- **header-only**, **tiny (99 lines)** and **powerful** ([USRefl_99.h](include/USRefl_99.h) (MSVC & GCC), [USRefl_99_clang.h](include/USRefl_99_clang.h) (Clang))
- **noninvasive** 
- basic
  - (non-static / static) member variable
  - (non-static / static) member function
- **attribute** 
- **enum** 
  - string <-> enumerator
  - static dispatch
- **template** 
- **inheritance** 
  - diamond inheritance
  - iterate bases recursively
  - virtual inheritance
- **parser** 

## Example

run it online : [**compiler explorer**](https://godbolt.org/z/7n6foG) 

```c++
#include <USRefl/USRefl.h>
#include <iostream>

struct Point {
  float x;
  float y;
};

template<>
struct Ubpa::USRefl::TypeInfo<Point> : TypeInfoBase<Point> {
  static constexpr AttrList attrs = {};
  static constexpr FieldList fields = {
    Field {TSTR("x"), &Type::x},
    Field {TSTR("y"), &Type::y},
  };
};

int main() {
  Point p{ 1.f, 2.f };
  Ubpa::USRefl::TypeInfo<Point>::ForEachVarOf(
    p,
    [](const auto& field, auto&& var) {
      std::cout << field.name << ": " << var << std::endl;
    }
  );
}
```

result is

```
x : 1
y : 2
```

**other example** 

- 99 line: [USRefl_99.h](include/USRefl_99.h), [test](src/test/06_99/main.cpp), [**online**](https://godbolt.org/z/h4zWEM) (test all examples below)
- [template](src/test/01_template/main.cpp) 
- [static](src/test/02_static/main.cpp) 
- [func](src/test/03_func/main.cpp) 
- [enum](src/test/04_enum/main.cpp) 
- [inheritance](src/test/05_inheritance/main.cpp) 
- [virtual inheritance](src/test/07_virtual/main.cpp) 
- [attribute name as type](src/test/10_type_attr/main.cpp) 
- AutoRefl : [app](src/AutoRefl), [example](src/test/09_AutoRefl/00_basic) ([Vec.h](src/test/09_AutoRefl/00_basic/Vec.h), Vec_AutoRefl.inl (generated by AutoRefl), [main.cpp](src/test/09_AutoRefl/00_basic/main.cpp))

## Documentation

- [Introduction](doc/intro.md) 
- parser (TODO) (check CMake option `Ubpa_USRefl_Build_AutoRefl` to generate the parser)

## Integration

You can choose one of the following two methods

- ⭐ **method 0**: add required file [USRefl_99.h](include/USRefl_99.h) for MSVC and GCC (use [USRefl_99_clang.h](include/USRefl_99_clang.h) for Clang)
- ⭐ **method 1**: cmake install, `find package(USRefl REQUIRED)` to get imported target `Ubpa::USRefl_core` 

## Compiler compatibility

- Clang/LLVM >= 10
- GCC >= 10
- MSVC >= 1926 (not fully support virtual inheritance because of [a MSVC bug](https://developercommunity.visualstudio.com/content/problem/1116835/member-pointer-of-a-class-with-a-virtual-base-1.html))

## Licensing

You can copy and paste the license summary from below.

```
MIT License

Copyright (c) 2020 Ubpa

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

