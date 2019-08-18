---
title: Swift auto diagram
date: 2017-03-01 00:00:00
author: 知识小集成员
cover: true
---

Swift auto diagram
----------

`OmniGraffle`无法绘制`Swift`的类图，只能再找个替代工具：`swift auto diagram`。这是一个ruby写的[开源库](https://github.com/yoshimkd/swift-auto-diagram)。

下载源码后，可以在工具所在目录下执行命令：

```ruby
ruby generateClassDiagram.rb ~/workspace/my-swift-project
```

然后会生成一个静态html页面，如图所示。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/03/6-1.png?raw=true)

可以看到其以不同颜色标出了`protocol`, `class`, `struct`, `extension`等类型及它们之间的关系。在这个页面里面可以自由地拖动类型框。嗯，不过，谈不上美观啊~~~

参考

[Swift Class Diagrams and more](https://martinmitrevski.com/2016/10/12/swift-class-diagrams-and-more/)