# poppy

This repository provides a C++ wrapper library for the C-API to control the Python interpreter and its sample code.

### API

Designed to it feels like calling a dynamic library.

Usage:
```cpp
// main.cpp (caller)

using namespace poppy;

// load script file
auto module = Import("calc");

// reserve function object
auto func = module.GetAttribute("multiply").ToFunc();

// run function
auto result = func(Int(2), Int(3)).ToValue();
```

```py
# calc.py (callee)

def multiply(a: int, b: int) -> int:
  c = 0
  for i in range(0, a):
    c = c + b
  return c
```

### Samples
1. [echo](samples/01_echo)
2. [calc](samples/02_calc)
3. [numpy](samples/03_numpy)
4. [struct](samples/04_struct)
5. [class](samples/05_class)
6. [thread](samples/06_thread)

### Requirements
* Python installation (>= 3.9) with numpy package
* C++ compiler
* CMake (>= 3.14)
* Visual Studio Code (with 'C/C++', 'CMake', 'CMake Tools' extensions)

NOTE: To build with Debug configuration, you need to install the Python debugger static library (python3xxd.lib). If not, only Release builds are available.

### Build and Run
1. In [settings.json](.vscode/settings.json), please edit 'PYTHONPATH' to your envirionment. If already registered, comment out this line.
2. Open this (top) directory by Visual Studio Code.
3. Do CMake 'Configure'.
4. Select target & launch (F5).

### References
* [Embedding Python in Another Application](https://docs.python.org/3/extending/embedding.html)
* [Python/C API Reference Manual](https://docs.python.org/3/c-api/index.html)