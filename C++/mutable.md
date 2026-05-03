# 在类中使用

```cpp
#include <iostream>
#include <string>

class Entity
{
private:
	std::string m_Name;
	mutable int m_DebugCount = 0;
public:
	Entity() = default;
	Entity(const char* name)
		: m_Name(name){}

	const std::string& GetName() const
	{
		m_DebugCount++;
		return m_Name;
	}
};

int main()
{
	Entity e = Entity("Cai");
	e.GetName();
		
	return 0;
}
```

# 在 lambda 表达式中使用

```cpp
#include <iostream>

int main()
{
	int x = 10;
	auto f = [=]() mutable
	{
		x++;
		std::cout << x << std::endl;
	};
	f();
	return 0;
}
```