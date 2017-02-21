---
title: C语言位运算
date: 2017-02-21 18:47:54
tags: [c, macro]
categories: c
---


```C
#define COMM_BIT_SET(a,b)     ((a) |= (1<<(b)))   // 将 a 的 b 位置1（1左移b位）
#define COMM_BIT_CLR(a,b)     ((a) &= ~(1<<(b)))  // 将 a 的 b 位清零
#define COMM_BIT_GET(a,b)     (!!((a) & (1<<(b)))) // 判断 a的b位是否置1 （!!用于将正数转为0或1）
```
<!-- more -->
COMM_BIT_SET与COMM_BIT_GET通常组合使用：

```C
enum {
  TEST1 = 1,
  TEST2 = 2,
};

int i = 0;
COMM_BIT_SET(i, TEST1);
cout<< COMM_BIT_GET(i, TEST1) <<endl;  // true
cout<< COMM_BIT_GET(i, TEST2) <<endl;  // false

COMM_BIT_SET(i, TEST2);
cout<< COMM_BIT_GET(i, TEST1) <<endl;  // false
cout<< COMM_BIT_GET(i, TEST2) <<endl;  // true

```
更多，[参见](http://imhuchao.com/423.html)
