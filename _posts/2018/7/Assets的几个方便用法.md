---
title: Assets的几个方便用法
date: 2018-07-01 00:00:00
author: 高老师很忙
cover: true
---

Assets的几个方便用法
----------
**作者**: [高老师很忙](https://weibo.com/517082456)

Assets想必大家都使用过，今天聊几个Assets比较方便的用法。

* 在工程中，某个通用的颜色，我们可能会用宏或者全局变量来表示，这样可以方便大家的使用，但有一个弊端，在`storyboard`或者`xib`布局的时候，设置颜色依旧要去设置具体的RGB值；而Assets给我们提供了一个很方便的功能，可以创建`New Color Set`，就弥补了刚才方案的缺陷（如图1，图2），并且代码中使用也很方便。

![](https://github.com/iOS-Tips/iOS-tech-set/blob/master/images/2018/07/2-1.jpg)

![](https://github.com/iOS-Tips/iOS-tech-set/blob/master/images/2018/07/2-2.jpg)

* 在需要拉伸图片的时候，通常会使用UIImage的API的`-[UIImage  resizableImageWithCapInsets:resizingMode:]`这个方法；而Assets为我们提供了Slicing的功能（如图3），在Assets中直接设置后，在storyboard和xib中就可以直接显示拉伸后的图片，在代码中使用也及其方便，直接用`-[UIImage imageNamed:]`方法即可。

![](https://github.com/iOS-Tips/iOS-tech-set/blob/master/images/2018/07/2-3.jpg)

* 如果是Universal的工程，同一个UIImageView，在iPhone中显示图片A，在iPad中显示图片B，Assets可以很方便的通过`Devices`设置，会让代码看着很清爽，不会存在判断机型再去设置图片的恶心代码。在设置横竖屏的时候也可以充分利用`Width Class`和`Height Class`两个参数（如图4）。

![](https://github.com/iOS-Tips/iOS-tech-set/blob/master/images/2018/07/2-4.jpg)

我觉得这3个用法在工作中还是很实用的，当然Assets还有其他很好用的功能，欢迎大家一起交流。