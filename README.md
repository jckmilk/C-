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
在这个简单的模型中，**一个object是一系列的slots，每一个slot指向一个members。Members按其生命次序**。各被指定一个slots。每一个data或function都有自己的一个slot。在这个简单的模型中，members并不放在objects中，只有指向member的指针才放在object中。
## 表格驱动对象模型
为了对所有的class的所有的objects都有一致的表达式，另一种对象模型是把所有与members相关的信息抽出来，放在一个data member table和一个member function talble之中。class object本身则内涵指向这两个表格的指针。member function table是一系列的slots 每一个slot指出一个member function；
data member table则直接含有data本身。
