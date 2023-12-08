### 01_echo

This sample shows the simplest usage.

* Python code:
```py:01_echo.py
def echo(message: str) -> tuple[str, str]:
  print("------ C++ -> Python ------")
  print(message)
  print()
  return message, "world"
```

* C++ code:
```cpp:main.cpp
#include "poppy.h"
#include <iostream>

using std::cout;
using std::endl;
using namespace poppy;

int main() {
  // first,
  Initialize();

  // relative path from workspace directory
  AddModuleDirectory("scripts");

  // load script file
  auto module = Import("01_echo");

  // reserve function object
  auto func = module.GetAttribute("echo").ToFunc();

  // run function
  auto tuple = func(Str("hello")).ToTuple();

  // print results
  cout << "------ Python -> C++ ------" << endl;
  std::cout
    << "Reply: "
    << tuple.Get(0).ToValue().ToString() << ", "
    << tuple.Get(1).ToValue().ToString() << "!" << std::endl;

  // after destructing all,
  Finalize();
  cout << "\n\n\n";
}
```

* Result:
```shell
------ C++ -> Python ------
hello

------ Python -> C++ ------
Reply: hello, world!
```