---
title: 动态加载Framework/Library
date: 2018-01-01 00:00:00
author: 南峰子_老驴
layout: post
---


在开发 `Framework/Library` 时，我们可能需要在 `Demo` 中测试不同版本的兼容性。如果每次都在 `Demo` 的 `Build Phase` 中切换 `Framework/Library` 的不同版本，是件很麻烦的事。这种情况下，我们就可以考虑在运行时动态加载 `Framework/Library`。方法很简单，就是使用 `"dlfcn.h"` 中的 `dlopen` 函数：

```objc
void *framework1Handle = dlopen("DynamicFramework1.framework/DynamicFramework1", RTLD_LAZY);
```

`dlopen` 有一个对应的方法 `dlclose` 用于卸载库，不过在 `iOS` 上，这个方法似乎不起作用。因此在同一次运行时，没有办法直接切换 `Framework/Library` 的不同版本，否则会出现如图的提示。实际使用哪个版本的代码无法确定。

```objc
objc[10662]: Class CASHello is implemented in both /private/var/containers/Bundle/Application/73362515-9CCA-47E0-B709-49BA437935DC/ios-dynamic-loading-framework.app/Frameworks/DynamicFramework1.framework/DynamicFramework1 (0x105680178) and /private/var/containers/Bundle/Application/73362515-9CCA-47E0-B709-49BA437935DC/ios-dynamic-loading-framework.app/Frameworks/DynamicFramework2.framework/DynamicFramework2 (0x105694178). One of the two will be used. Which one is undefined.
```

变通的方案是在启动时提供一个选择页面，选择在运行 `App` 时，使用哪个版本的 `Framework/Library`。如果要切换版本，再重新启动 `App` 。

`dlopen` 仅限于开发阶段使用。
