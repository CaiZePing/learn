单一变量存放多种类型的数据

```cpp
#include <iostream>
#include <variant>

int main()
{
	// 可以有更多类型
	std::variant<std::string,int> data;
	data = "Cat";
	std::cout << std::get<std::string>(data) << std::endl;
	data = 22;
	std::cout << std::get<int>(data) << std::endl;
	
	// 比较好的判断类型的方式
	if(auto value = std::get_if<std::string>(&data))
	{
		std::cout << "string" << std::endl;
	}else if(auto value = std::get_if<int>(&data))
	{
		std::cout << "int" << std::endl;
	}
	
	// 还可以这样访问
	switch(data.index())
	{
	case 0:
		std::cout << "string" << std::endl;
		break;
	case 1:
		std::cout << "int" << std::endl;
		break;
	default:
		std::cout << "false" << std::endl;
		break;
	}
}
```

