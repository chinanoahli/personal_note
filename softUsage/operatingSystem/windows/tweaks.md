# Windows 常用技巧

## 修复文件或路径无权访问的情况

我曾经在我电脑上用两个不同的硬盘安装了相同版本的 Windows 10 系统，并且使用了一个相同的用户名 `chinanoahli`

但是不久后，我发现，每次当我换不同的硬盘启动是，系统完成用户账户登录并进入桌面后，总会提示 **某分区的回收站损坏**

起初我不以为意，认为是不同系统的用户UID不一样，所以造成了这个盘的回收站出现了一些问题

所以我总是根据系统提示，把该盘符里面的回收站重建

但是渐渐地，我发现事情不太对劲，这个盘符出现了以下情况

+ 应用程序可以创建文件却无法写入<br>例如：用 **OBS Studio** 录屏，生成的文件始终是 `0 KB` 大小
+ 应用程序无法读取文件<br>例如：用 **VLC Player**播放某些mkv文件，VCL总是提示文件无法读取，可能是权限问题

经过长时间搜索无果后，偶然看到了[cfan上的一篇文章](https://www.cfan.com.cn/2020/1013/134391.shtml)，才确定是 *<i>盘符根目录的权限出错</i>* 所致

因为盘符根目录是它里面所有子目录的父目录，所以 *<i>盘符根目录</i>* 的权限出错将会被继承到所有的子目录中，但是你在Explorer中却不能看出问题所在，而且一般来说，也不能一下子就想到竟然是 *<i>盘符根目录</i>* 的权限出现了错误

为了修复这个错误，你可以通过拥有 *<i>管理员权限</i>*  的终端运行以下命令解决：

```shell
takeown /f X: /A /R /D Y
::         ^ 将 `X` 改为你出错的盘符
```

## 禁用新网络位置提示

当电脑连接到一个新的网络环境时，Windows 总会提示：

```
想要允许你的电脑被此网络上的其他电脑和设备发现吗?

我们建议你在家庭和工作网络而非公共网络上启用此功能。
```

如果你在某些虚拟机上使用Windows，那么很有可能，这个提示每次开机都会遇到

你可以通过创建下面一个注册表 *项*，来禁用这个烦人的提示

```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Network\NewNetworkWindowOff]
```

## 将硬件时间设定为UTC

Windows 默认将主板 RTC 模块的时间识别为当地时间，而 \*UNIX 则是识别为 UTC 时间

这样会导致 Windows 和 \*UNIX 双系统使用时，总会有一个系统产生很大时差

为了解决这个问题，可以通过新增下面的注册表*键值* 来解决

```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation]
"RealTimeUniversal"=hex(b):01,00,00,00,00,00,00,00
```

---

[上一级](../README.md)

[笔记首页](../../../README.md)