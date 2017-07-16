---
title: C++对C的扩展
date: 2017-07-16 10:51:55
tags: C++
categories: cpp
---
C++在C的基础上进行了扩展，如扩展了bool类型，表达式可以被赋值等等
<!--more -->
#### 扩展了bool类型等
C语言中表示真假用非0与0，而C++中扩展使用true与false，实际上的bool类型是一个枚举变量，如下：
```C++
#include <iostream>
using namespace std;
enum BOOL
{   
    FALSE,TRUE
};
int main()
{
    bool b = false;
    BOOL bb = FALSE;
    cout<<"b:"<<b<<",bb:"<<bb<<endl;
    cout<<"sizeof(b):"<<sizeof(b)<<",sizeof(bb):"<<sizeof(bb)<<endl;
    return 0;
}

// 结果如下：
b:0,bb:0
sizeof(b):1,sizeof(bb):4

```

#### 一些表达式可以被赋值
C++的表达式可以赋值，是因为运算符重载的缘故，如++i，重载++运算符，return \*this， 可以继续赋值。注意：此处i++不可当做左值，因为 return int。
```C++
#include <iostream>
using namespace std;
int main()
{
    int a, b=5;
    (a=b) = 10;    // C语言中编译不通过
    cout<<"a:"<<a<<",b="<<b<<endl;
    (a!=b? a:b) = 1000;              // C语言中编译不通过
    cout<<"a:"<<a<<",b="<<b<<endl;

    int i = 0;
    ++i = 10;      // C语言中编译不通过
    cout<<"i:"<<i<<endl;
    return 0;
}

//结果：
a:10,b=5
a:1000,b=5
i:10
```
如果在使用C语言编译上述表达式，则会出现：
```C
test.c: In function ‘main’:
test.c:5:11: error: lvalue required as left operand of assignment
     (a=b) = 10;
           ^
test.c:6:17: error: lvalue required as left operand of assignment
     (a!=b? a:b) = 1000;
                 ^
test.c:9:9: error: lvalue required as left operand of assignment
     ++i = 10;
         ^
```
