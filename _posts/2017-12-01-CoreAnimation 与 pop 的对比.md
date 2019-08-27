---
title: CoreAnimation 与 pop 的对比
date: 2017-12-01 00:00:00
author: 知识小集成员
layout: post
---

最近在 `Medium` 上看到一篇《Should you use POP?》的文章，文章主要通过以下几个方面来对比了 `pop` 和 `Core Animation`。

* `Core Animation` 工作原理：每次添加动画时 `QuartzCore` 会打包其参数，然后通过进程间通信的方式传递给一个名为 `backboardd` 的后台进程。然后该进程通过 `OpenGL` 渲染和处理 `layer` 的层级以及 `layer` 上的动画。最重要的一点就是该进程完全独立于你的应用，应用只会拿到动画开始和结束的回调（`CAAnimationDelegate`），不负责动画的渲染（显式动画除外）。也就是主线程和 `CoreAnimation` 不会互相影响，也就是即使主线程阻塞了，`CoreAnimation` 依旧在执行。

* `pop` 的工作原理：使用 `CADisplayLink` 来开启一个 `fps=60` 的渲染工作。每当 `CADisplayLink` 回调触发时，更新一下动画的进度。也就是每一帧发生改变时都需要通知 `backboardd` 来渲染，因为它对于 `layer` 的变化并不知情。

* 由于 `pop` 必须在主线程上处理动画，所以 `pop` 动画很有可能发生卡顿。作者写了一个 `Demo` 来演示对应效果，效果如下图，左边为 `Core Animation` 的方式，右边为 `pop` 的方式。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/12/9-1.gif?raw=true)

* 作者对比了 `Core Animation` 和 `pop` 的性能。同样动画效果情况下(运行10s)，使用 `Time Profiler` 看 `backboardd` (`CoreAnimation`) 和应用(`pop`) `CPU` 消耗，`iPhone4 iOS7.1.2` 和 `iPhone6 iOS8.1.1` 的对比结果下图所示（左边 `iPhone4`，右边 `iPhone6`）。可以看出两者 `backboardd` 进程的 `CPU` 耗时差别在 `100ms` 左右，但是应用的 `CPU` 耗时差距十分明显，`Core Animation` 应用 `CPU` 耗时接近于0。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/12/9-2.jpg?raw=true)

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/12/9-3.jpg?raw=true)

* 结论如下图所示。`Core Animation` 优点为：①单独进程运行 ②不会阻塞主线程。缺点为：①复杂动画效果要写冗长的代码 ②手势驱动动画比较复杂。 `pop` 的优点为：①丰富的 API ②内置很多的动画 缺点为：①在主线程上执行 ②动画过程可能卡顿 ③消耗更高的 `CPU`

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/12/9-4.jpg?raw=true)
