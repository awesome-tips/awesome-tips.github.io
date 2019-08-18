---
title: iOS 11中隐藏section头尾的实现
date: 2017-11-01 00:00:00
author: iOS_OneByte
cover: true
---

iOS 11中隐藏section头尾的实现
----------

**作者**: [iOS_OneByte](https://weibo.com/u/5549095051)

iOS 中 `UITableView` 中有一种比较常用的样式 `UITableViewStyleGrouped`。有时我们要隐去 `section` 头尾的话，经常实现如下：

```objc
- (CGFloat)tableView:(UITableView *)tableView heightForHeaderInSection:(NSInteger)section
{
    return 0.1f;
}

- (CGFloat)tableView:(UITableView *)tableView heightForFooterInSection:(NSInteger)section
{
    return 0.1f;
}
```

如果只实现这2段代码的话，在 `iOS 11` 之前是不会出现问题的，但 `iOS 11` 之后需要同时实现如下：

```objc
- (UIView *)tableView:(UITableView *)tableView viewForHeaderInSection:(NSInteger)section
{
    return nil;
}

-(UIView *)tableView:(UITableView *)tableView viewForFooterInSection:(NSInteger)section
{
    return nil;
}
```

`Base SDK` 路径设置： `Xcode` < `Build Settings` <  `Base SDK`

`Base SDK`：指得是当前编译应用的和构建 `.ipa` 的 `SDK` 的版本，并且手机的 `SDK` 版本是向前兼容。