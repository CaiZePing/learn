>[!CAUTION] 注意  
>千万不要在头文件中使用 `using namespace`

使用这个关键字，有时会出现意想不到的事情发生
如果要使用，最好在一个小的作用域中使用

```cpp
#include <iostream>
#include <string>

namespace apple {
	void print(const std::string & text){
		std::cout << text << std::endl;
	}
}

namespace orange {
	// 这是一个恶意程序
	void print(const char* text){
		std::string temp = text;
		std::reverse(temp.begin(),temp.end());
		std::cout << temp << std::endl;
	}
}

using namespace apple;
using namespace orange;

int main()
{
	// 如果想用 apple 中的函数
	// 但是这样使用，会使用 orange 中的 print 函数
	print("hello");
	// 但是这样使用永远不会有歧义
	apple::print("hello");
	orange::print("hello");
	
	return 0;
}
```