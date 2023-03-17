# 42 this关键字 in C++

`this`是一个指向当前对象实例的指针。

在构造函数赋值时，最好使用`this`；尤其当函数列表参数与成员变量名字一样时，必须得使用了。

```c++
void PrintEntity2(Entity2* e);
void PrintEntity2(Entity2 & e)

class Entity2{
public:
	int x, y;
	Entity2(int x, int y)
	{
		// Entity2 * e = this;         //该类型的一个指针，指向当前对象
		this->x = x;
		this->y = y;
		(*this).x = x;                //对指针解引用后赋值，和上面的效果是一样的，通常还是按上面的那么写
		(*this).y = y;
	
        PrintEntity2(this);         //很好的诠释了this的意义，指向当前对象的指针
        PrintEntity2(*this);        //参数是引用，就传入解引用
    
    
    }
};

void PrintEntity2(Entity2* e)
{

}

```

xxxxxxxxxx struct Vector{    int X, Y;​    Vector(int x,int y)        :X(x),Y(y){}​    Vector Add(const Vector& other)const    {        return Vector(X + other.X, Y + other.Y);      //在return里直接调用构造函数，代码非常简练    }​    Vector operator + (const Vector& other)const    {        return Add(other);                        //可以直接调用Add()    }        bool operator == (const Vector& other) const    {        return X == other.X && Y == other.Y;               //简练，要记得这么写​    }    bool operator != (const Vector& other) const    {        //return !operator==(other);            //也对，但是比较奇怪        return !(*this == other);    //使用重载过的== 操作符​    }​    std::ostream & operator << (std::ostream& stream,const Vector&other)  const     //重载<<运算符,这里提示函数参数过多    {        stream << other.X << " " << other.Y << std::endl;        return stream;    }​};​Vector v1(2, 3);Vector v2(1, 2);Vector result=v1 + v2;​std::cout << result << std::endl;c++
