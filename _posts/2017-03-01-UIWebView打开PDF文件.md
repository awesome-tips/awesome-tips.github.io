---
title: UIWebView打开PDF文件
date: 2017-03-01 00:00:00
author: 知识小集成员
layout: post
---


`UIWebView`可以直接打开PDF文件，代码很简单，如下所示：

```swift
@IBOutlet weak var webView: UIWebView!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        let filename = Bundle.main.path(forResource: "test", ofType: "pdf")
        let url = URL(fileURLWithPath: filename!)
        
        let request = URLRequest(url: url)
        self.webView.scalesPageToFit = true
        self.webView.loadRequest(request)
    }
```

效果如下图所示：

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/03/4-1.png?raw=true)

加载的PDF文件是放置在一个`UIWebPDFView`视图中，`UIWebPDFView`应该是一个私有类，可以在 [UIWebPDFView.h](https://github.com/nst/iOS-Runtime-Headers/blob/master/Frameworks/UIKit.framework/UIWebPDFView.h)查看其声明。
