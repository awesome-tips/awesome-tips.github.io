---
title: 提高Shortcuts调试效率的小技巧
date: 2018-07-01 00:00:00
author: 高老师很忙
layout: post
---
iOS12提供了`Shortcuts`的功能，今天给大家介绍2个苹果提供的提高`Shortcuts`调试效率的小技巧。

* `Shortcuts`是可以通过Siri唤起的，如果每次调试的时候都要和Siri说一次短语，既浪费时间又打扰旁边正在工作的同事，Xcode提供了`Siri Intent Query`功能，在调试`Intents Extension`或者`Intens UI Extension`的target时，直接在里面输入你要说的短语，就可去省去调戏Siri的时间啦。

![](https://github.com/iOS-Tips/iOS-tech-set/blob/master/images/2018/07/4-1.png?raw=true)

* 在`iPhone设置`->`开发者`里面提供了`Display Recent Shorts`和`Display Donations on Lock Screen`的开关，可以忽略系统当前的建议和预测，显示我们需要调试的`Shortcuts`；同时还支持`Force Sync Shortcuts to Watch`的功能，手动去强制同步到Watch，会节省很多时间哦！

![](https://github.com/iOS-Tips/iOS-tech-set/blob/master/images/2018/07/4-2.png?raw=true)

我觉得这2个小技巧还是很实用的，如果有其它小技巧欢迎一起交流！
