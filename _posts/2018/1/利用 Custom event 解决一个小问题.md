---
title: 利用 Custom event 解决一个小问题
date: 2018-01-01 00:00:00
author: 拿破仑的风火轮_
cover: true
---

利用 Custom event 解决一个小问题
--------
**作者**: [_拿破仑的_风火轮_](https://weibo.com/u/2293476232)

做IM开发时,有个场景是:数据异步处理,回到主线程刷新UI、展示消息给用户看到.当用户短时间内收到很多条消息时,我们不想对UI进行频繁而累赘的更新,理想的情况是当主线程繁忙时将所有的改变联结起来。此时,可以利用联结的优势(在异步线程上调用 `dispatch_source_merge_data` 后，就会执行 `dispatch source` 事先定义好的 `handler` )。使用 `DISPATCH_SOURCE_TYPE_DATA_ADD`，将刷新UI的工作拼接起来，短时间内做尽量少次数的刷新。

伪代码

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2018/01/20-1-1.png?raw=true)

执行结果

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2018/01/20-1-2.png?raw=true)

欢迎大家分享其他思路.