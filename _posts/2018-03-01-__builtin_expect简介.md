---
title: __builtin_expect简介
date: 2018-03-01 00:00:00
author: 高老师很忙
layout: post
---

`__builtin_expect` 是 `GCC` 引入的，对if语句的预言，用这个指令告诉编译器最有可能执行的代码，从而编译器进行优化，通俗来讲就是告诉编译器执行 `if` 和 `else` 哪个是大概率事件。话不多说直接说用法：`__builtin_expect(EXP, N)`，很简单，`EXP == N` 是大概率事件。

我先用正常的写法写了一个简单的的Demo

![](https://github.com/iOS-Tips/iOS-tech-set/blob/master/images/2018/03/11-1.png?raw=true)

代码执行时间是0.017361秒；加上这个指令

![](https://github.com/iOS-Tips/iOS-tech-set/blob/master/images/2018/03/11-2.png?raw=true)

代码执行时间是0.007645秒，还是挺明显的。小伙伴们也来试试哇！
