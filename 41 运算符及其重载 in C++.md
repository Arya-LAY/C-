# 41 运算符及其重载 in C++

运算符是一种我们使用的一种符号，通常代替一个函数来执行一些事情。运算符就是一种函数。

重载：给运算符赋予新的含义，或者添加参数，或者创建。

重载`+`里调用了`Add()`函数，一般项目里都写上。

```c++
struct Vector
{
	int X, Y;

	Vector(int x,int y)
		:X(x),Y(y){}

	Vector Add(const Vector& other)const
	{
		return Vector(X + other.X, Y + other.Y);      //在return里直接调用构造函数，代码非常简练
	}

	Vector operator + (const Vector& other)const
	{
		return Add(other);                        //可以直接调用Add()
	}
    
    bool operator == (const Vector& other) const
	{
		return X == other.X && Y == other.Y;               //简练，要记得这么写

	}
	bool operator != (const Vector& other) const
	{
		//return !operator==(other);            //也对，但是比较奇怪
		return !(*this == other);    //使用重载过的== 操作符

	}

	std::ostream & operator << (std::ostream& stream,const Vector&other)  const     //重载<<运算符,这里提示函数参数过多
	{
		stream << other.X << " " << other.Y << std::endl;
		return stream;
	}

};

Vector v1(2, 3);
Vector v2(1, 2);
Vector result=v1 + v2;

std::cout << result << std::endl;
```