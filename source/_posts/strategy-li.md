---
title: strategy模式
date: 2017-08-14 19:39:59
tags: [设计模式, 李建中]
categories: 设计模式
---

如果代码中存在变化可扩展的 if...else 逻辑的硬编码，当新增一种逻辑分支时，须修改源码适配，维护较为困难。此时可通过该策略模式来解决。

<!-- more -->
详细介绍，可参见。
[策略模式](http://design-patterns.readthedocs.io/zh_CN/latest/behavioral_patterns/strategy.html)

注意：关键词 变化，可扩展（此处条件判断分支，随需求变化，需不断扩展条件分支情形；如果条件语句固定，如一周7天，此时无需使用该模式）

```C++
/*************************************************************************
	> File Name: main.cpp
	> Author: ma6174
	> Mail: ma6174@163.com
	> Created Time: Mon 14 Aug 2017 05:10:06 AM PDT
 ************************************************************************/
#include "Strategy.h"
#include "Context.h"
#include "ConcreteStrategyA.h"
#include "ConcreteStrategyB.h"
#include<iostream>
using namespace std;

int main()
{
	ConcreteStrategyA *pCSA = new ConcreteStrategyA();
	ConcreteStrategyB *pCSB = new ConcreteStrategyB();

	Context *pContext = new Context();
	pContext->SetStrategy(pCSA);
	pContext->Algorithm();

	pContext->SetStrategy(pCSB);
	pContext->Algorithm();

	delete pCSA;
	delete pCSB;
	delete pContext;

	return 0;
}

/*************************************************************************
	> File Name: Context.h
	> Author: ma6174
	> Mail: ma6174@163.com
	> Created Time: Mon 14 Aug 2017 05:06:44 AM PDT
 ************************************************************************/
#ifndef __CONTEXT__H__
#define __CONTEXT__H__

#include "Strategy.h"
#include<iostream>
using namespace std;

class Context
{
public:
	void SetStrategy(Strategy* cStrategy)
	{
		m_cStrategy = cStrategy;
	}
	void Algorithm()
	{
		m_cStrategy->Algorithm();
	}

private:
	Strategy *m_cStrategy;
};
#endif


/*************************************************************************
	> File Name: Strategy.h
	> Author: ma6174
	> Mail: ma6174@163.com
	> Created Time: Mon 14 Aug 2017 05:02:15 AM PDT
 ************************************************************************/
#ifndef __STRATEGY__H
#define __STRATEGY__H

#include<iostream>
using namespace std;

class Strategy
{
public:
	virtual ~Strategy(){}
	virtual void Algorithm() = 0;

};

#endif


/*************************************************************************
	> File Name: ConcreteStrategyA.h
	> Author: ma6174
	> Mail: ma6174@163.com
	> Created Time: Mon 14 Aug 2017 05:03:31 AM PDT
 ************************************************************************/
#ifndef __ConcreteStategy__H__
#define __ConcreteStategy__H__

#include "Strategy.h"
#include<iostream>
using namespace std;

class ConcreteStrategyA:public Strategy
{
public:
	virtual ~ConcreteStrategyA(){}
	virtual void Algorithm()
	{
		cout<<"ConcreteStrategyA."<<endl;
	}
};

#endif

```
