---
title: 关于UIStackView的一个小知识点
date: 2019-01-01 00:00:00
author: 高老师很忙
cover: true
---

关于UIStackView的一个小知识点
----------
**作者**: [高老师很忙](https://weibo.com/517082456)

今天分享一个`UIStackView`的小知识点,用`UIStackView`做水平或垂直布局很方便，搜了大多数UIStackView的资料，大多是教大家如何使用的axis、alignment等属性的。最近使用时遇到了：把`UIStackView`中某个视图`hidden`后，`UIStackView`的布局会进行更新，只展示没有`hidden`的视图（官方文档截图：图1），

![](https://github.com/awesome-tips/iOS-Tips/blob/master/images/2018/12/3-1.png)

例如，你有5个视图平等分显示，设置某个视图`hidden`之后，就会变成4个视图平等分了。

有的时候这是我们期许的，而有的时候并不是；如果`hidden`某个视图后，不想更改其他视图布局，那么可以设置alpha，或者使用`Masonry`的方法，之前小集也提过（图2）。

![](https://github.com/awesome-tips/iOS-Tips/blob/master/images/2018/12/3-2.png)

了解这个属性之后，免得大家开发过程走弯路，根据情况选择适当的方式布局。