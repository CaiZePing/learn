不需要通过函数定义，就可以定义一个函数的方法
在有函数指针的情况下都可以使用 **lambda**

# 基础使用

```cpp
#include <iostream>
#include <vector>

void Foreach(const std::vector<int> &values, const std::function<void(int)> &func)
{
	for (int value : values)
		func(value);
}

int main()
{
	std::vector<int> values = {2, 532, 343, 5, 32223, 23};
	
	auto it = std::find_if(values.begin(), values.end(), [](int value){ return value > 533; });
	
	std::cout << *it << std::endl;
	
	int a = 10;
	
	auto lambda = [=](){ std::cout << a << std::endl; };
	
	lambda();
	
	Foreach(values, [](int value){ std::cout << value << std::endl; });
}
```