# 40 隐式转换与explicit关键字

## Entity类

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

## 正常创建对象及实例化

```c++
Entity a("arya");      // 调用第二个构造函数
Entity b(22);          //调用第三个构造函数
```

## 涉及隐式转换的创建对象及实例化

```c++
Entity b = 22;
```

隐式构造函数：将22转换成一个`Entity`，因为`Entity`类中有一个接受`int`类型参数的构造函数。

xxxxxxxxxx struct Vector{    int X, Y;​    Vector(int x,int y)        :X(x),Y(y){}​    Vector Add(const Vector& other)const    {        return Vector(X + other.X, Y + other.Y);      //在return里直接调用构造函数，代码非常简练    }​    Vector operator + (const Vector& other)const    {        return Add(other);                        //可以直接调用Add()    }        bool operator == (const Vector& other) const    {        return X == other.X && Y == other.Y;               //简练，要记得这么写​    }    bool operator != (const Vector& other) const    {        //return !operator==(other);            //也对，但是比较奇怪        return !(*this == other);    //使用重载过的== 操作符​    }​    std::ostream & operator << (std::ostream& stream,const Vector&other)  const     //重载<<运算符,这里提示函数参数过多    {        stream << other.X << " " << other.Y << std::endl;        return stream;    }​};​Vector v1(2, 3);Vector v2(1, 2);Vector result=v1 + v2;​std::cout << result << std::endl;c++

例如，`const char*`到 `string` 到 `Entity`

```c++
Entity a = "arya";     //❌，因为“arya”是const char * 类型，到达Entity中间还有一步。
Entity a = std::string("arya");     //✔ ，string默认构造函数，将字符串显示转换为string类型，c++隐式的转换为Entity
Entity a = Entity("arya");      //✔，将const char *隐式转换为string,然后调用构造函数
```

## explicit关键字：禁止隐式调用构造函数

C++编译器默认支持隐式转换的。有时需要禁止隐式转换，这就是`explicit`存在的意义。

```c++
explicit Entity(int age)
		:m_Name("Unknown"),m_Age(age){}

Entity b = 22;         //会报错，不能从int转换为Entity
```

### 总结：除非必要，可以不用隐式转换，就正常的创建对象及实例化。

