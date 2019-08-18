---
title: Shell脚本在iOS中的应用
date: 2017-11-01 00:00:00
author: Lefe_x
cover: true
---

Shell脚本在iOS中的应用
----------

**作者**: [Lefe_x](https://weibo.com/u/5953150140)

使用 Pod 的同学经常会遇到 `"error: The sandbox is not in sync with the Podfile.lock. Run 'pod install' or update your CocoaPods installation."` 错误，如下图所示。其实是 `[CP] Check Pods Manifest.lock` 这个脚本所起的作用。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/11/5-1.PNG?raw=true)

Pod 中有 `Manifest.lock` 和 `Podfile.lock` 这两个文件，只要这两个文件的内容不一样就会报错上面这个错误。`Podfile.lock` 是大家共用的文件（用来保证我们每个人的Pod库版本一样），而 `Manifest.lock` 是本地的文件（自己用）。下图中这个脚本正是做这样的事情。

```shell
diff "${PODS_PODFILE_DIR_PATH}/Podfile.lock" "${PODS_ROOT}/Manifest.lock" > /dev/null
if [ $? != 0 ] ; then
    # print error to STDERR
    echo "error: The sandbox is not in sync with the Podfile.lock. Run 'pod install' or update your CocoaPods installation." >&2
    exit 1
fi
# This output is used by Xcode 'outputs' to avoid re-running this script phase.
echo "SUCCESS" > "${SCRIPT_OUTPUT_FILE_0}"

```

**解释下这个脚本**

`shell` 脚本总是以：`#!/bin/bash` 或者 `#!/bin/sh` 开头，它主要告诉系统执行这个文件需要哪个解释器，进入 `/bin` 目录下可以看到 bash 和 sh 解释器；

- `diff` 命令：判断两个文件的不同，比如 `diff /Users/lefe/Desktop/project/Kmart/Podfile.lock /Users/lefe/Desktop/project/Kmart/pods/Manifest.lock >~/Desktop/shell.log` 比较两个文件的不同，并重定向到 `shell.log` 文件中；
- `>` 重定向符号，可以把输出命令输出到某个文件中而不是控制台；
- `echo` 是脚本的输出，相当于 `printf`；
- `exit 1` 退出，有了这个命令 Xcode 就会报错，你可以在 Xcode 中新建一个脚本，试试下面这个脚本：

```shell
echo "This is a test shell created by Lefe_x"
exit 1
```

- `$?：` 指上条命令执行的结果，也就是 `diff` 执行的结果；

- 下面是 shell 中的 if 语句：

```shell
if 条件 ; then
fi
```

**如何在终端执行脚本**

假如有个叫 `podlgsk.sh` 的脚本，只要给予它执行权限（`chmod +x podlgsk.sh`），注意只需要给一次执行权限就行，下次运行脚本时就不需要给予执行权限了，然后直接 `./podlgsk.sh` 即可。

**小结**

其实 `Shell` 脚本就是把一些 `linux` 命令组合到一起，经过一些处理（比如：if 判断，循环等）后所形成的文件。（不知道总结的是否恰当）