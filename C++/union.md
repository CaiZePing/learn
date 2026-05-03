一个相同内存的变量，可以翻译成不同的类型变量

# 类型双关

```cpp
#include <iostream>

int main()
{
	int a = 10;
	// 隐式转换为 double
	double d1 = a;
	// 将 a 以二进制的形式映射为 double
	double d2 = *((double*)(char*)&a);
	double &d3 = *((double *)(char *)&a);
	// d1 值为 10
	std::cout << d1 << std::endl;
	// 这两个值为 -6.39512e-46
	std::cout << d2 << std::endl;
	std::cout << d3 << std::endl;
	
	return 0;
}
```

# union

```cpp
#include <iostream>

struct Vector2
{
	float x,y;
};

struct Vector4
{
	float x,y,z,m;
};

void printVector2(const Vector2&v)
{
	std::cout << v.x << ", " << v.y << std::endl;
}

struct Vector4_u
{
	union
	{
		struct
		{
			float x,y,z,m;
		};
		struct
		{
			Vector2 a,b;
		};
	};
};

int main()
{
	// 这边就是类型双关的 union 实现
	std::cout << "============Basic=========" << std::endl;
	
	union
	{
		int a;
		float b;
	} value;
	value.a = 10;
	
	std::cout << "int = " << value.a << std::endl;
	std::cout << "float = " << value.b << std::endl;
	// 类型双关 和 union 对 类的用法
	std::cout << "============Vector========" << std::endl;
	
	Vector4 v4 = {1.0f, 2.0f, 3.0f, 4.0f};
	printVector2(*(Vector2 *)&v4);
	printVector2(*((Vector2 *)&v4 + 1));
	
	std::cout << "--------------------------" << std::endl;
	
	Vector4_u v4u = {1.0f, 2.0f, 3.0f, 4.0f};
	printVector2(v4u.a);
	printVector2(v4u.b);
}
```