`const` 基本上就像你做出的承诺，它承诺某些东西将是不变的

# 变量中

```cpp
#include <iostream>

int main()
{
	int a = 5;
	const int b = 10;
	int const c = 15;
	const int * d = a;
	int *const e = a;
	const int * f = a;
	const int *const g = a;
	// 所有注释的都是错的
	// 赋值
	a = 50;
	// b = 50;
	// c = 50;
	d = &b;
	// e = &b;
	f = &b;
	// g = &b;
	
	// 修改数值（指针）
	// *d = 30;
	*e = 30;
	// *f = 30;
	// *g = 30;
	
	return 0;
}
```

# 类中

```cpp
#include <iostream>

class Entity
{
private:
	int m_X,m_Y;
	mutable int m_Num;
public:
	int GetX()const
	{
		// 这是允许的
		// mutable 关键词允许成员变量可以在
		// const 修饰的函数中
		// 修改变量值
		m_Num = 10;
		return m_X;
	}
	int GetX()
	{
		return m_X;
	}
	void SetX(int x)
	{
		m_X = x;
	}
};

void PrintEntityConst(const Entity&e)
{
	// 这边会调用 const 修饰的重载函数
	// 这边要使用保证变量不可修改的函数
	// 如果不是 const 修饰的函数
	// 可能在内部会修改成员变量
	std::cout << e.GetX() << std::endl;
}

void PrintEntity(Entity&e)
{
	// 这边会调用 没有 const 修饰的函数重载
	// 因为这个函数中允许修改类中的成员变量
	std::cout << e.GetX() << std::endl;
}

int main()
{
	Entity e;
	e.SetX(10);
	PrintEntityConst(e);
	PrintEntity(e);
	
	return 0;
}
```