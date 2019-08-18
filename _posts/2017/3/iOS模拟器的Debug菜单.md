---
title: iOS模拟器的Debug菜单
date: 2017-03-01 00:00:00
author: 知识小集成员
cover: true
---

iOS模拟器的Debug菜单
----------

iOS模拟器的`Debug`菜单中提供了几个菜单项来检测影响帧率的一些因素：

1. `Color Blended Layers`: 高亮显示有混合操作的区域；
2. `Color Copied Images`: 高亮显示被拷贝的图片。拷贝图片意味着`Core Animation`需要拷贝一份图片并发送给`render server`，这对内存和CPU的使用都是昂贵的；
3. `Color Misaligned Images`: 高亮显示缩放或拉伸过的图片，或者没有正确对齐对到像素边界的图片；
4. `Color Offscreen-Rendered`: 高亮显示离屏渲染的层对象。

当然这几个选项在`Instrument`的`Core Animation`工具中也可以找到。

参考

iOS Core Animation Advanced Techniques