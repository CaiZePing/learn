正常情况用不到

```cpp
#include <iostream>
#include <any>

int main()
{
    std::any data;

    data = 2;
    int a = std::any_cast<int>(data);
    std::cout << a << std::endl;
    // 注意这个是 const char*
    data = "Cai";
    const char * str = std::any_cast<const char*>(data);
    std::cout << str << std::endl;
}
```
