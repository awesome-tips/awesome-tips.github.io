---
title: Gerrit 是阻挡不了你使用 SourceTree
date: 2017-12-01 00:00:00
author: Lefe_x
layout: post
---

当我们提交的代码需要 Review 的时候，需要用到 Gerrit，具体关于 Gerrit 的介绍可以看 [这里]
(https://gerrit-review.googlesource.com/Documentation/) 。使用 Gerrit 后，执行 `push` 操作的时候，不能直接使用 `git push` 命令，也就说你不能使用 `SourceTree` 的 `Push` 功能，只能在终端乖乖的输入 `git push origin HEAD:refs/for/dev` 。有些同学可能会问，我特别想使用 `SourceTree` ，不想使用终端命令，有没有好的方法？其实，`SourceTree` 提供了一个功能：【自定义操作】（SourceTree -- 偏好设置 -- 自定义操作 -- 添加），导入事先写好的脚本。还可以设置一个快捷键（这里设置了 cmd+p）。脚本如下：

```
#!/bin/bash
cd /Users/wangsuyan/Desktop/iOS
git push origin HEAD:refs/for/Dev0.0.1
```

备注：记得给脚本执行权限。
如果你没有给自定义的操作设置快捷键，可以通过【动作 -- 自定义操作】选择执行你的 Action。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/12/3-1.jpg?raw=true)

这样，当你 push 的时候直接 `cmd+p` 即可提交你的代码，是不是很爽。当然你可以写一些其它的脚本，并自定义为 Action ，来提高你的工作效率。你可以看我以前写的 [脚本教程] (http://www.jianshu.com/p/8a975f358de8) 。
