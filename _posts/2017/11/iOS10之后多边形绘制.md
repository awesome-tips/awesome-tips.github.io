---
title: iOS10之后多边形绘制
date: 2017-11-01 00:00:00
author: Vong_HUST
cover: true
---

iOS10之后多边形绘制
----------

**作者**: [Vong_HUST](https://weibo.com/VongLo)

众所周知，对于一些多边形的绘制，我们可以使用 `CAShapeLayer` 配合 `UIBezierPath`，然后再用这个 `layer` 给 `View` 做 `mask` 即可。但是一种情况是不行的，对于 `UIVisualEffectView`，iOS10 之前 `self.blurView.layer.mask = someShapeLayer` 这一句是 ok 的，但是 iOS10 之后，这样设将无效，而应该使用 `self.blurView.maskView = maskView`。具体代码如下图所示：

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/11/6-1.JPG?raw=true)

详细解释可参考[这里](https://forums.developer.apple.com/thread/50854)