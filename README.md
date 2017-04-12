### [TCLAP](http://tclap.sourceforge.net/) support for tuples

This small repository is an extension of TCLAP for supporting `std::tuple` with `ValueArg` by creating 
a template specialization for:

```cpp
namespace TCLAP {
    template<class... Args>
    class ValueArg<std::tuple<Args...>>;
}
```

To use this extension, simply include the `tclapt.h` file in your source:

```cpp
#include <iostream>

#include "tclapt.h"

int main(int argc, char *argv[]) {
    TCLAP::CmdLine cmd("Example.", ' ', "0.1");
    TCLAP::ValueArg<std::tuple<int, int>> itvArg(
        "i", "interval",
        "Minimum and maximum values.",
        false, std::make_tuple(0, 100), "int int", cmd);
    cmd.parse(argc, argv);
    
    auto itv = itvArg.getValue();
    
    std::cout << "Found: " << std::get<0>(itv) << "< " << std::get<1>(itv) << '\n';
}
```

You can then run command like this:

```
./exec -i 0 20
```
