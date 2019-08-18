---
title: 点击cell不执行-[UITableView didSelectRowAtIndexPath:]方法的几种方式
date: 2019-01-01 00:00:00
author: 高老师很忙
cover: true
---

点击cell不执行-[UITableView didSelectRowAtIndexPath:]方法的几种方式
----------
**作者**: [高老师很忙](https://weibo.com/517082456)

今天分享一个比较常用的知识点，点击某个UITableViewCell不执行`-[UITableView didSelectRowAtIndexPath:]`方法的几种方式：

- 可以直接设置`cell.userInteractionEnabled = NO`；

- 可以实现UITableViewDelegate中的`-[UITableView shouldHighlightRowAtIndexPath:]`方法，设置对应indexPath返回NO；

![](https://github.com/awesome-tips/iOS-Tips/blob/master/images/2019/01/10-1.jpg)
	
- 可以实现UITableViewDelegate中的`-[UITableView willSelectRowAtIndexPath:]`方法，设置对应indexPath返回nil，不过这种方式cell还是会有高亮效果，需要手动设置对应`cell.selectionStyle = UITableViewCellSelectionStyleNone`；


以上三个方法，都不会进UITableViewDelegate的`-[UITableView didSelectRowAtIndexPath:]`方法。用第一种方式设置后，cell上的所有子View都不能被点击了；而第二种方式不会影响cell的子View的响应事件的传递，如果cell上有UIControl的子类，依然可以被点击；第三种方式也不会影响cell的子视图的响应事件，但是需要额外设置不显示高亮效果。当然，你也可以在`-[UITableView didSelectRowAtIndexPath:]`方法的对应indexPath直接return，只要你高兴😂，可以根据实际情况选择合适的方法。

有更优雅的方式，欢迎一起讨论。