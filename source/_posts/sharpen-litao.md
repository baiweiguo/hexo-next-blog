---
title: 锐化
date: 2017-08-04 20:27:35
tags: ps
categories: ps
---


PS三种锐化效果：常规锐化，精细化锐化，质感锐化。------- 李涛《数码摄影后期高手之路》

<!-- more -->
### 常规锐化（高反差保留）

1.复制一个图层，使用高反差保留滤镜
2.图像叠加

### 精细化锐化（推荐）

1.锐化对象：LAB模式中的亮度通道，以减少彩色溢出情况。锐化是增加对比度，可能造成高光溢出
2.使用2次USM锐化。一次半径大一些5，一次半径小一些1.2

### 质感锐化

1.生成两个背景图层；
2.其中一个使用表面模糊；
3.另外一个使用应用图像，减去表面模糊图层，得到颗粒图像；
4.叠加图像
