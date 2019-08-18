---
title: JSManagedValue对底层Javascript值的引用 
date: 2017-09-01 00:00:00
author: 知识小集成员
cover: true
---

JSManagedValue对底层Javascript值的引用
----------

使用`JSManagedValue`保存值时，需要注意其底层的`Javascript`值的使用。

`JSManagedValue`添加了"条件保留(`conditional retain`)"机制为值提供自动内存管理，不过需要使用`JSVirtualMachine`的`addManagedReference(_:withOwner:)`方法。如果没有的话可能会导致一些问题，因为`JSManagedValue`行为类似于`ARC`的`weak`引用，所以当`Javascript`的垃圾收集器把`JSManagedValue`的底层`Javascript`值销毁时，`JSManagedValue`对象的`value`属性会自动变成`nil`。

下面是我写的一个Bug：

```javascript
// action为局部变量
const action = function () {
	window.location.href = 'https://www.baidu.com';
	setTimeout(() => {
		api.setMenu([]);
	}, 300);
};

appApi.setMenu([{
	menuTitle: '订单',
	menuAction: action,
}]);
```

`menuAction`是一个`Javascript`回调函数，在`iOS`代码中用一个`JSManagedValue`来包装`menuAction`值，但由于`menuAction`是一个局部变量，所以一定时间会被回收；这时如果想再从`JSManagedValue`中取出`menuAction`回调来执行，由于其值已变成`nil`，所以不会产生任何效果。

还是得多读读文档啊。

参考

1. [JSManagedValue Reference](https://developer.apple.com/documentation/javascriptcore/jsmanagedvalue)