---
title: C++函数重载
date: 2017-07-22 20:48:27
tags: cpp
categories: cpp
---

C++函数重载的原理，是c++编译器在利用name mangling技术（倾轧），来修改函数名，区分参数不同名字相同的函数。
重命名时使用 v-c-i-f-l-d表示void,char,int,float,long,double参数及其引用。
<!-- more -->
    ```C++
    nm a.out |grep func
    00000000004006e0 T _Z4funci     // 使用C++编译，函数没有用extern "C" 修饰，倾轧

    nm a.out |grep func
    00000000004006e0 T func         // 使用C++编译，函数使用extern "C" 修饰，不倾轧
    ```

#### C++函数重载（静多态）
函数名相同，函数参数列表不同：类型，个数，顺序。函数重载使用时，允许如下两种匹配原则：

* 严格参数类型匹配
  函数参数，使用强制类型转换
* 参数使用隐式类型转换
  需注意：double 可隐式转化为int float，可引起二义性，编译不通过。（或这int隐式转long double）
  ```C++
  #include<iostream>
  using namespace std;
  void func(int a)
  {
  	cout<<a<<endl;
  }
  void func(float a)
  {
  	cout<<a<<endl;
  }
  int main()
  {
  	func(4.5); // 4.5默认double类型，可使用 func(4.5f);
  	return 0;
  }  
  ```
  ```C
  // 编译出错：
  func.cpp: In function ‘int main()’:
  func.cpp:22: error: call of overloaded ‘func(double)’ is ambiguous
  func.cpp:11: note: candidates are: void func(int)
  func.cpp:16: note:                 void func(float)

  //使用 func(4.5f)时，则编译通过：
  nm a.out |grep func
  00000000004008d0 t _GLOBAL__I__Z4funci
  000000000040084d T _Z4funcf
  0000000000400824 T _Z4funci
  ```

#### C++兼容C库
C++使用extern "C"修饰函数, 可使函数不进行倾轧，用于兼任C库使用。注：如果声明和定义位于不相关文件中，则声明和定义处均须使用。
```C++
// main.cpp文件
extern "C" void func(int a);
int main()
{
	func(3.5);
	return 0;
}

// func.cpp文件
#include <iostream>
using namespace std;
extern "C" void func(int a)
{
	cout<<a<<endl;
}
```

```C
//若 func.cpp文件中无 extern "C"修饰 func，则：
/tmp/cc3LVVzf.o: In function `main':
test.cpp:(.text+0xa): undefined reference to `func'
collect2: ld returned 1 exit status
//若 声明extern "C"位于单独的头文件，main.cpp, func.cpp都引用该头文件，func.cpp未使用 extern "C"，也可以编译通过。
```
---------------本笔记来自于《带你实战C++》
