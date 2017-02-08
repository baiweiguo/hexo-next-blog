---
title: 静态成员函数调用非静态成员变量
date: 2017-02-07 16:14:49
tags: [c++, static]
categories: c++
---

　　一般使用情况下，类静态成员函数调用静态成员变量，不能调用非静态变量，否则编译器会出错。因为非静态成员属于类对象，只有在类对象的实例创建时，才会分配内存，然后通过对象进行访问；而静态成员属于整个类，不需要类对象的创建，此时使用静态成员访问非静态成员好比访问内存中不存在的东西。

<!--more -->
　　静态成员调用静态成员的一般方法：

```C++
#include <iostream>
using namespace std;

class CStatic
{
public:
    static void Print()
    {
        cout<<m_iTest<<endl;
    }
private:
    static int m_iTest; //此处为静态成员变量声明
};

int CStatic::m_iTest = 0; // 此处为定义，必须定义，否则编译出错。此处亦可用 int CStatic::m_iTest; 代替

int main(int argc, char* argv[])
{
    CStatic cs;
    cs.Print();
    return 0;
}
```


　　使用上述方式，有个问题，就是**需要对静态成员变量预先在类外定义，若成员变量个数较多，逐个定义起来比较麻烦**。此时，可使用静态成员调用非静态成员方法，[参见](http://www.cnblogs.com/rickyk/p/4238380.html)：

```C++
#include <iostream>
using namespace std;

class CStatic
{
public:
    CStatic()
    {
        m_iTest = 0;
        s_pInstance = this;   // 构造函数初始化
    }
    static void Print()
    {
        s_pInstance->m_iTest += 1;  //
        cout<<s_pInstance->m_iTest<<endl;
    }
private:
    int m_iTest;
    static CStatic* s_pInstance;
};
CStatic* CStatic::s_pInstance = NULL ;
int main(int argc, char* argv[])
{
    CStatic cs;   // 已加载到内存，构造函数中有参数this进行初始化（相当于c语言先定义变量，再调用函数）
    cs.Print();
    CStatic cs1;
    return 0;
}

```
