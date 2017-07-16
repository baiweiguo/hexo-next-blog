---
title: C++类型安全增强
date: 2017-07-15 13:36:48
tags: c++
categories: cpp
---

C++相对于C语言而已，是一种强类型语言，类型检查更严格。
<!-- more -->
#### 严格的类型检查
如，C语言中，可以使用一些“技巧”来更改常量的值，如下代码可直接运行：
```C
#include <stdio.h>
int main()
{
    const int a ;          // C语言可不初始化，定义后也不允许赋值
    printf("before. a:%d\n", a);
    int *p = &a;          // C语言，左右两边类型不同，允许编译通过
    *p = 10;              // 可赋值  
    printf("after. a:%d\n", a);
    return 0;
}
```
![hosts](cpp_type/Selection_002.png)

而在C++中，则不允许，强类型检查就会让编译都不通过：
![](cpp_type/Selection_001.png)

#### 真正的枚举
C语言中，可以对枚举变量进行任意赋值，而C++中，只能用枚举的元素进行赋值。
```C++
enum SEASON
{
    Spr = 1,
    Sum,Autu,Win
};

int main()
{
    SEASON s;
    cout<<s<<endl;
    s = Spr;         // C++中正确赋值
    cout<<s<<endl;
    s = 1;           // C++中赋值编译报错
    cout<<s<<endl;
    return 0;
}
```
![](cpp_type/Selection_003.png)
