---
title: Core Animation中CPU操作的影响因素
date: 2017-03-01 00:00:00
author: 知识小集成员
layout: post
---


`Core Animation`中CPU的操作在动画开始前执行，所以通常不会影响到动画的帧率，但是会影响到动画的开始。以下一些操作会延迟动画的开始时间：

1. 布局计算：这可以理解，视图越复杂，需要的计算量越大。特别注意`auto layout`是一种CPU密集型操作，比传统的`autoresizing`更耗CPU；
2. 延迟加载视图机制：这个机制带有两面性，优点是优化内存使用和启动时间；缺点的涉及到IO操作；
3. `Core Graphics`绘制：自定义的`-drawRect:`或`-drawLayer:inContext:`会引入显著的性能开销；因为`Core Animation`会在内存中创建一个与视图等大小的`backing image`用来绘制，然后再通过`IPC`将这个图片数据发送给`render server`；
4. 图片解压。

参考

iOS Core Animation Advanced Techniques
