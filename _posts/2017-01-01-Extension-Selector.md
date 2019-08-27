---
title: Extension-Selector
date: 2017-01-01 00:00:00
author: 知识小集成员
layout: post
---


在`Swift`中，我们可以使用`#selector`设置`target-action`模式中的`action`操作，如下代码所示：

```swift
class ViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
        
        let button = UIButton(type: .custom)
        button.addTarget(self, action: #selector(buttonTapped), for: .touchUpInside)
        
        view.addSubview(button)
    }

    func buttonTapped() {
        
    }
}
```

如果你有代码洁癖，想把`#selector`集中起来管理，则可以定义一个结构体，来统一归集这样的代码，如下图所示。这样看着是不是会更整洁一些？

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/01/21-1-1.png?raw=true)

不过，还有种更好的方式，就是直接扩展`Selector`结构体，如下代码所示，这样可以在使用时直接用`.buttonTapped`这种方式来引用，就像我们使用`.red`这样的`UIColor`属性一样简洁。

```swift
extension Selector {
    static let buttonTapped = #selector(ViewController.buttonTapped)
}

class ViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
        
        let button = UIButton(type: .custom)
        button.addTarget(self, action: .buttonTapped, for: .touchUpInside)
        
        view.addSubview(button)
    }

    func buttonTapped() {
        
    }
}
```

参考

[Swift: Selector Syntax Sugar](https://medium.com/swift-programming/swift-selector-syntax-sugar-81c8a8b10df3#.md6860mmq)
