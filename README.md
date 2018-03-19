# C++ 对象模型
1. 语言中直接支持面向对象程序设计的部分
2. 对于各种支持的的底层实现机制
在C++中，有两种class data members：static和nonstatic，以及三种class member functions：static、nonstatic和virtual。
```
class Point{
public:
    Point(flaot xval);
    virtual ~Point();
    float x() const;
    static int PointCount();
protected:
    virtual ostream& print(ostream &os) const;
    float x_;
    static int _point_count;
};
```

## 简单对象模型
![简单对象模型](https://raw.githubusercontent.com/jckmilk/C-object-model/master/%E7%AE%80%E5%8D%95%E6%A8%A1%E5%9E%8B.jpg)
在这个简单的模型中，**一个object是一系列的slots，每一个slot指向一个members。Members按其生命次序**。各被指定一个slots。每一个data或function都有自己的一个slot。在这个简单的模型中，members并不放在objects中，只有指向member的指针才放在object中。
## 表格驱动对象模型
![member function 模型](https://raw.githubusercontent.com/jckmilk/C-object-model/master/member%20function.jpg)
为了对所有的class的所有的objects都有一致的表达式，另一种对象模型是把所有与members相关的信息抽出来，放在一个data member table和一个member function talble之中。class object本身则内涵指向这两个表格的指针。member function table是一系列的slots 每一个slot指出一个member function；
data member table则直接含有data本身。
## C++对象模型
![c++d对象模型](https://raw.githubusercontent.com/jckmilk/C-object-model/master/C%2B%2B%E5%AF%B9%E8%B1%A1%E6%A8%A1%E5%9E%8B.jpg)
C++对象简单模型从简单对象模型派生，在此模型中，**nonstatic data member被配置在每个class object之内，static data member则被存放在所有的class object之外 static和nonstatic function members也被放在所有的class object之外，virtual function则以两个步骤支持：**
1. 每一个class产生一堆指向virtual function的指针，放在表格之中 ，这个表格被称为 virtual table。
2. 每一个class被添加一个指针，指向相关的virtual table。通常这个指针被称为vptr。vptr的设定和重置都由每一个class的constructor、destructor和copy assignment运算符自动完成。每一个class所关联的type_info object也经常由virtual table指出。
## 加上继承
单一继承
```
class Library_materials{...};
class Book:public Library_materials{...};
class Renta_book:public Book{...};
```
多重继承
```
class iostream:
public istream, public ostream
{...};
```
虚拟继承（virtual）
```
class istream:virtual public ios {...};
class ostream:virtual public ios {...};
```
在虚拟继承中 base class不管在继承串链中被派生多少次 永远只会存在一个实体，例如iostream 之中就只有virtual ios base class的一个实体。
# 对象模型如何影响程序
