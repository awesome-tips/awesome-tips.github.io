---
title: 当 iTerm 遇上 ZSH，他们相爱了
date: 2017-11-01 00:00:00
author: Lefe_x
cover: true
---

当 iTerm 遇上 ZSH，他们相爱了
----------

**作者**: [Lefe_x](https://weibo.com/u/5953150140)

> Your terminal never felt this good before.

上一条 `iOS知识小集` 主要说了下使用 `iTerm` 可以改善我们的终端，评论中 [@CrespoXiao](https://weibo.com/crespoxiao) 和 [@struggleend](https://weibo.com/u/3106903737) 提到了 `iTerm + ZSH` 使用起来更方便。搜了下 `ZSH`，发现 Star 数 62476 个，确实是好东西，和大家分享下，目前使用时间不长，姑且总结几条我认为比较好的，有熟悉的同学在评论中分享给大家吧 🤝，相信同学们不会吝啬的。[安装看这里](https://github.com/robbyrussell/oh-my-zsh/) 。`Oh My Zsh` 它是基于 zsh 命令行的一个扩展工具集。

提示：根目录下有 `~/.zshrc` 文件，可以修改配置，比如主题，插件等。

- 设置一个主题，如果你有洁癖，选择一个你认为比较好的[主题](https://github.com/robbyrussell/oh-my-zsh/wiki/Themes) ；
- 使用插件，比如有 Git 插件，当记不住命令的时候，按 Tab 键可以提示，比如 `git p [tab]` 将会提示，如下图所示；

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/11/17-1.png?raw=true)

- 支持简写，比如省略 cd，回到上级目录直接输入：.. ；
- `ls *.jpeg`  显示当前目录下所有 jpeg 文件；
- `cd <TAB>` 简显示当前目录下的文件，继续按 <TAB> 可以选择你所要进入的目录；
- `git <UP>` 可以找到最近输入的 Git 命令；

想了解 `ZSH` 更多特性，可以查看 [官网](http://ohmyz.sh/)