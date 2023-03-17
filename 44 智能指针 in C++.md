# 44 智能指针 in C++

### 智能指针

智能指针的行为类似于常规指针，区别在于他复杂内存的自动释放，当对象超过其作用域时。

某个时刻只能有一个`unique_ptr`指向一个给定的对象。当`unique_pyr`被销毁时，它所指向的对象的也会被销毁。

### `unique_ptr` 

作用域指针，超过作用域时，就会调用delete。

该指针不能复制，只能是唯一的。因为如果复制的话，会有两个指针指向同一片区域，当其中有一个释放后，另一个指针会指向一块已经释放的区域，这显然是不行的。

基本没有什么开销。

使用`unique_pt`r时，`#include<memory>`

```c++
#include<iostream>
#include<string>
#include<memory>

class Entity
{
public:
	Entity()
	{
		std::cout << "Created Entity!" << std::endl;
	}
	~Entity()
	{
		std::cout << "Destroyed Entity!" << std::endl;
	}
};

int main()
{
	{
		std::unique_ptr<Entity>entity(new Entity());
		//std::unique_ptr<Entity>entity3 = new Entity();         //unique_ptr必须显式调用构造函数

		std::unique_ptr<Entity>entity2 = std::make_unique<Entity>();  //这种调用方式更安全
	}
	//超过这个作用域时，指针就会被自动释放。

}
```

> ### shared_ptr

允许多个`shared_ptr`指针指向同一个对象。同时会分配一个引用计数。每`copy`一个，引用计数就会`+1`。当引用计数`=0`时，对象被销毁。

会有一点开销，因为维护了一个引用计数。

### weak_ptr

当该指针由`shared_ptr`赋值来的时候，`shared_ptr`的引用计数不会增加。