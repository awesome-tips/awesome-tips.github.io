---
title: Autolayout Theory
date: 2017-02-01 00:00:00
author: 知识小集成员
layout: post
---


`View hierarchy`的`layout`可以定义为一系列的线性方程式。每个约束都表示一个方程式，大部分约束定义的是两个视图之间的关系，当然也可以是一个视图的两个不同的属性之间的关系，如高宽比。

下图是文档中给出的一个等式样例，

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/02/18-1-1.png?raw=true)

下图是一个基本的解释，

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/02/18-1-2.png?raw=true)

参考

1. [Auto Layout Guide](https://developer.apple.com/library/content/documentation/UserExperience/Conceptual/AutolayoutPG/AnatomyofaConstraint.html#//apple_ref/doc/uid/TP40010853-CH9-SW1)
