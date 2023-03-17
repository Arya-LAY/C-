# 39 new关键字 in C++

### 在编写c++程序语言时，应该关心内存、性能和优化问题。如果不在乎这些的话，真的不必使用这个语言，其他的语言会更简单方便。

## new的主要目的是在堆上分配内存

### <u>**new  数据类型**</u>

#### 无论是基本数据类型，还是类类型，还是数据）类型决定了在内存中会分配多大的空间。

#### 例如，new int ,向操作系统请求，给我一个4字节的连续的内存块，找到内存块后，返回一个指向这个内存的指针。这也可以看出，new比较消耗时间）

## <u>new其实一种操作符，delete也是,要记得手动释放new分配的空间。</u>

### Entity类

```c++
class Entity
{
private:
	String m_Name;
	int m_Age;
public:
	Entity()
		:m_Name("Unknown"),m_Age(-1){}

	Entity(const String& name)
		:m_Name(name),m_Age(-1){}

	 Entity(int age)
		:m_Name("Unknown"),m_Age(age){}

	
	const String& GetName()const
	{
		return m_Name;
	}
};
```

### new 和delete操作符的使用

new在分配内存的同时，还可以调用构造函数。

```c++
int a = 2;   //在栈上分配
int* b = new int;    //在堆上分配4字节
int* c = new int[2];    //在堆上分配数据，占内存4x2=8字节

Entity* entity = new Entity[5]; //分配数据

Entity* entity2 = new Entity();    //new不仅分配内存，还调用了构造函数

delete entity2;
delete[] entity;     //释放数组
delete[] c;
delete b;
```

