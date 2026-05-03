处理数据是否存在

```cpp
#include <iostream>
#include <fstream>
#include <optional>
#include <string>
#include <sstream>

// 读取文件内容并返回optional<string>
// 如果文件打开失败则返回空optional
std::optional<std::string> ReadFileString(const std::string &filepath)
{
	std::ifstream stream(filepath);
	if (stream)
	{
		std::stringstream buffer;
		// 将文件内容读取到stringstream中
		buffer << stream.rdbuf();
		stream.close();
		// 返回包含文件内容的optional
		return buffer.str();
	}
	// 文件打开失败，返回空optional
	return {};
}

int main()
{
	// 尝试读取文件
	std::optional<std::string> data = ReadFileString("data.txt");
	
	// 使用value_or获取值，如果data为空则使用默认值"hello world"
	std::string value = data.value_or("hello world");
	std::cout << "Content: " << value << std::endl;
	
	// 检查文件是否读取成功
	if (data)
	{
		std::cout << "File read successfully" << std::endl;
		// 两种访问optional中数据的方式
		std::string &content = *data;
		std::cout << "Length: " << data->length() << std::endl;
	}
	else
	{
		std::cout << "File could not be opened" << std::endl;
	}
	return 0;
}
```