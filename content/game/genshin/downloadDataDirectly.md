---
title: "抓取原神数据包的下载地址"
date: 2023-05-05T19:14:32+09:00
draft: false
---

# 抓取原神数据包的下载地址

> 参考链接：[点我跳转(需翻墙)](https://oscarcx.com/tech/genshin-direct-download.html)
>
> 这里原作者说方法已失效，实际上是错误的，直到`3.3.0`更新为止，本方法仍然有效

## 0x00 工具的准备

首先我们要准备工具，以从内存提取下载地址

不用担心，这个过程是安全的，因为没有篡改游戏本身的文件，也不需要登录（只操作启动器），所以正常来说不会被封禁

工具的名字叫 **<i>Process Hacker</i>** ，官方网站点[这里](https://processhacker.sourceforge.io/)，进入官网后，点击网页上蓝色的按钮 **<i>Download Process Hacker</i>** ，然后根据你的系统以及架构选择对应的 *Portable* 版本即可

> *Portable* 即便携版，不需要安装，下载后是一个zip压缩文件，解压到任意位置即可使用

## 0x01 启动 Process Hacker 的注意点

一定要记得用管理员身份运行Process Hacker，否则Process Hacker将无法读取原神启动器的内存，从而造成操作失败

![Access Denied](https://github-share-1304366332.cos.ap-guangzhou.myqcloud.com/game/genshin/attachments/access_denied.png)

## 0x02 通过 Process Hacker 启动原神启动器

在解压出来的Process Hacker路径中找到`ProcessHacker.exe`，然后右键点击它，从弹出菜单中选择`以管理员身份运行 (A)`

> 请注意，如果你成功地以管理员身份运行了Process Hacker的话，它的标题栏是会显示`Administrator`的（见下图）

然后你将会看到Process Hacker的主窗口

![Main Window](https://github-share-1304366332.cos.ap-guangzhou.myqcloud.com/game/genshin/attachments/mainWindow.png)

现在，从菜单栏中找到`Hacker > Run...`，然后从弹出文件选择窗口中，选择原神启动器的`launcher.exe`以通过 Process Hacker 启动原神启动器

然后让启动器开始下载数据文件，如初次安装游戏或进行预下载等等

![Run Launcher from PH](https://github-share-1304366332.cos.ap-guangzhou.myqcloud.com/game/genshin/attachments/run.png)

这时我们先将注意力放到Process Hacker的主窗口中，从进程列表里面找到原神图标的`launcher.exe`进程

找到之后，在它上面点击鼠标右键，并从弹出菜单中选择`Properties`，打开启动器进程的属性窗口

在属性窗口中，我们进入`Memory`标签，然后点击`Strings...`按钮

接下来会弹出 **String Search** 字符串搜索窗口，这里我们不需要更改任何设置，直接点击`OK`按钮即可

![Open Properties](https://github-share-1304366332.cos.ap-guangzhou.myqcloud.com/game/genshin/attachments/properties.png)

接着在弹出的 **Results** 结果窗口中，点击窗口左下角的`Filter`过滤器按钮，并在弹出的菜单中选择`Conntains`内容

![Filter](https://github-share-1304366332.cos.ap-guangzhou.myqcloud.com/game/genshin/attachments/filter.png)

然后在弹出的**Filter**过滤器窗口中填入`autopatch`这串字符，并点击`OK`按钮

![Autopatch](https://github-share-1304366332.cos.ap-guangzhou.myqcloud.com/game/genshin/attachments/autopatch.png)

接下来，Process Hacker将会弹出新的 **Results** 结果窗口，我们可以看到很多以`.zip`结尾的文件链接

如何选择下载链接，将会在下一段讲述，这里我们先学习一下如何把想要的链接复制出来

首先我们在 **Results** 窗口点击一条想要复制的链接选中它，然后点击窗口右下角的`Copy`按钮即可将这条结果复制出来

![Copy the Links](https://github-share-1304366332.cos.ap-guangzhou.myqcloud.com/game/genshin/attachments/links.png)

复制出来将会是以下的效果

```txt
0x18bf6416f90 (232):

https://autopatchcn.yuanshen.com/client_app/download/pc_zip/20221024103540_fp3L3cHoDpo9eNeT/Audio_Japanese_3.2.0.zip
```

我们只需要将第二行的链接复制到任意多线程HTTP下载工具开始下载即可

> 多线程HTTP下载工具：IDM、FDM等等都行

## 0x03 下载链接的选择

> 本次以3.2.0升级到3.3.0这次升级为例

在上面一步中，我们是先开始了在原神启动器里面下载任务再提取地址的

现在，我们可以打开游戏的安装目录，可以发现里面有一个后缀名为`zip_tmp`的文件

`tmp`即临时文件的意思，所以下载完成后后缀名里面的`_tmp`会被去掉，文件会自动被重命名为`*.zip`

这个就是我们即将要下载的数据文件，记下它的名字`game_3.2.0_3.3.0_hdiff_06STMj1gxyYbPCR5.zip_tmp`

从文件的名字中，我们可以看到我们目前的版本号为`3.2.0`，即将升级到`3.3.0`，而`hdiff`就是增量包的意思

> 增量包：只包含这次升级新增或修改的部分文件，并不包含整个游戏的全部文件
>
> 全量包：包含整个游戏的所有资源文件
>
> 所以如果你是初次下载安装游戏，就需要直接找到文件名不包含`hdiff`且版本号为最新版本的文件下载链接
>
> 如`YuanShen_3.30.zip`、`YuanShen_3.30.zip.001`等等，这里是分卷压缩，注意要把所有所有分P全部下完才行

然后我们就可以到Process Hacker的搜索结果里面，找到下载链接结尾为`game_3.2.0_3.3.0_hdiff_06STMj1gxyYbPCR5.zip`的链接，这就是我们要找了更新补丁数据链接

> 你现在或许发现了，Process Hacker的搜索结果里面还包含了从`3.1.0`升级到`3.2.0`的数据文件下载地址
>
> 假如你并没有先在启动器里开始下载任务，或者游戏安装目录里面没有找到临时文件，这里就要注意不要选错地址了！

要注意的是，这只是游戏本身的更新数据，并不包含不同的语言包和语音包

你可能已经注意到，Processs Hacker的搜索结果里面，包含很多语言代码，如`zh-cn`、`en-us`以及`ja-jp`

没错，就是相关的语言包，下面列出常见的语言代码：

+ `zh-cn` 代表简体中文
+ `en-us` 代表美国英语
+ `ja-jp` 代表日语
+ `ko-kr` 代表韩语

你会发现，好像没有见到有繁体中文的项目，这里我的推测是：繁体中文其实是由简体中文进行简单的简繁转换而来的

接下来还要处理语音包，再次浏览Process Hacker的搜索结果，我们可以发现，有不少文件是以`Audio`开头的，如`Audio_Chinese_3.3.0.zip`和`Audio_English(US)_3.3.0.zip`等等，这些文件的名字就好理解多了：

+ `Chinese` 代表中文语音包
+ `English(US)` 代表美式英语语音包
+ `Japanese` 代表日语语音包
+ `Korean` 调表韩国语语音包

根据自身的需要下载对应的语音包即可

## 如何处理下载到的数据文件

当我们把下载地址都找全了以后，就可以暂停原神启动器里面的下载任务，或干脆退出启动器

接下来进入游戏安装目录，把现有的后缀名为`zip_tmp`临时文件全部删除掉

然后把下载得到的文件的后缀名从`zip`改为`zip_tmp`，并将数据文件放到游戏目录（最好的做法是在下载时直接将游戏安装目录选为下载目录），再重新启动原神启动器，并重新开始下载任务

此时，原神启动器将会自动检查临时文件临时文件是否完整，如果文件完整的话，启动器将会自动解压并将新数据整合到现有的游戏数据里面

> 注意：我个人不推荐自己手动解压覆盖文件的做法，因为不确定米忽悠有没有在更新时进行文件的修改工作（如文件拼接等等），让启动器去自动处理最为保险

---

[上一级](..)

[笔记首页](/)