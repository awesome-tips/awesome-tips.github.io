---
title: UITextFile和UITextView的textContentType属性新类型
date: 2017-09-01 00:00:00
author: Lefe_x
layout: post
---

`UITextFile`和`UITextView`的`textContentType`属性新加了`UITextContentTypeUsername`和 `UITextContentTypePassword`类型，这样当你登录`App`时可以自动填充你的账号和密码，前提是你保存过密码到`Safari`或钥匙串。`App`可以和你的网站进行关联，如果在网站上登录过，可以自动填充密码和账户到你的`App`。

```objc
_textField.textContentType = UITextContentTypeUsername;
_textField.textContentType = UITextContentTypePassword;
```

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017-09-22-1-1.jpg?raw=true)
