---
title: 解决React Native引入realm导致编译卡顿问题
date: 2017-11-01 00:00:00
author: 知识小集成员
cover: true
---

解决React Native引入realm导致编译卡顿问题
----------

在`React Native`项目中引入`realm`后，在编译阶段，网络状况不好的时候会卡在realm模块下载的地方。现象是如果在终端用`react-native run-ios`，则会卡在`Download realm-sync-cocoa-${version}.tar.xz`，如果是Xcode，则会卡在`Build ${ProjectName}: RealmJS`这一块。

这主要是因为realm的库太大(`realm-sync-cocoa-${version}.tar.xz`包大概是50+M)。所以我们可以考虑把包先下载到本地，以减少每次编译的时间。

1. 我们可以从`realm-cocoa`的[build.sh文件](https://github.com/realm/realm-cocoa/blob/master/build.sh#L289)中找到`realm-sync-cocoa-${version}.tar.xz`的下载地址(注：${version}是具体的版本号)，下载文件。
2. 在命令行输入`getconf DARWIN_USER_TEMP_DIR`，获取文件下载的临时目录
3. 将下载的文件拷贝到临时目录
4. 这样基本就OK。

如果还不行，则可以考虑以下操作：

1. 修改下载的脚本代码了。找到`node_modules/realm/scripts/download_realm.js`；
2. 找到`download()`函数，将其中的`saveFile()`函数作如下修改；

```javascript
function saveFile() {
	if (process.stdout.isTTY) {
		printProgress(response.body, parseInt(response.headers.get('Content-Length')), archive);
	} else {
		console.log(`Downloading ${archive}`);
	}
	
	return new Promise((resolve) => {
		// const file = fs.createWriteStream(destination);
		// response.body.pipe(file).once('finish', () => file.close(resolve));
		resolve();
	}).then(() => fs.utimes(destination, lastModified, lastModified));
}
```

最后运行`react-native run-ios`。

参考

1. [Core occasionally cannot be downloaded from China](https://github.com/realm/realm-cocoa/issues/2713)