---
title: "绘画、动画资料库"
date: 2023-11-21T19:40:08+09:00
draft: false
---

# 绘画、动画资料库 {#drawingAndAnimationResourcesLibrary}

## 建立初衷

众所周知，国内共享资料的方式总是受到了很多限制：

例如常用的 *百●网盘* 会进行文件内容的审查，不符合规定的内容会导致无法分享，被爆就会死掉

再例如 *QQ群共享* ，空间小，管理查找困难，经常因为各种原因而无法刷新出文件列表等等

在例如 *115* ，虽然容量大，但基本不具备分享功能，使用不便等等……

于是本了便打算利用家里的 NAS 为大家创建一个可以让大家都可以快乐使用，免费的资源共享库

对比了几个共享工具，最后决定使用 *[Resilio Sync](https://www.resilio.com/individuals)* ，来作为资料库的共享平台，[原因见此处](#选择-resilio-sync-的原因)

接下来就直接介绍资料库的使用办法：

## 资源库使用办法

首先进入 Resilio Sync 的官网下载并安装 Sync Home 软件<sub>(软件官网被墙，此处省略一万字，并提供[备用连接](#软件下载))</sub>，并自行完成安装

此处以Windows版作为示例，其他系统参考对照操作即可：

1. 打开 Resilio Sync 然后点击右上角的 `⚙️齿轮` 图标进入设置<br>在 **<i>General > Language</i>** 里面把语言设置为 `简体中文` <br>然后关闭软件窗口，最后双击任务栏托盘区的 Resilio Sync 重新打开软件的窗口<br>这样可以把软件改成中文的了<br>![切换语言](https://github-share-1304366332.cos.ap-guangzhou.myqcloud.com/art/drawingAndAnimationResources/attachments/img001.png)
2. 点击设置里面的 `许可证 > 应用许可证` ，并在弹出的选择文件窗口打开下载到的 `ResilioSyncPro.btskey` 文件，以便激活软件的高级功能<br>![打开许可证](https://github-share-1304366332.cos.ap-guangzhou.myqcloud.com/art/drawingAndAnimationResources/attachments/img002.png)<br>![激活后](https://github-share-1304366332.cos.ap-guangzhou.myqcloud.com/art/drawingAndAnimationResources/attachments/img003.png)
3. 点击软件窗口左上角的 `+` 按钮，然后选择 `输入密钥或链接`<br>![添加共享](https://github-share-1304366332.cos.ap-guangzhou.myqcloud.com/art/drawingAndAnimationResources/attachments/img004.png)
4. 然后在手动连接里面输入密钥 `BNLPW4YZDIYO4NJNC6QP4NUXSOBJVWCGG` ，并把**<i>选择性同步</i>**设为 `On`，然后点击 `下一步` <br>![输入密钥](https://github-share-1304366332.cos.ap-guangzhou.myqcloud.com/art/drawingAndAnimationResources/attachments/img005.png)<br><sub>(若你想成为做种团队的一员，则不需要打开选择性同步，若不打开选择性同步，就会把整个资源库同步到硬盘上)</sub>
5. 接下来软件会弹出 *选择文件夹* 窗口，在这里选择你要存放共享库的地方，例如在我的例子中是 `E:\Resilio Sync\Drawing.and.Animation.Resources`<br>![选择存放路径](https://github-share-1304366332.cos.ap-guangzhou.myqcloud.com/art/drawingAndAnimationResources/attachments/img006.png)
6. 这样一来就设置完成了，软件窗口会列出你刚设置的同步文件夹<br>![共享文件夹列表](https://github-share-1304366332.cos.ap-guangzhou.myqcloud.com/art/drawingAndAnimationResources/attachments/img007.png)
7. 稍等片刻，进入刚才设置的文件夹，可以看到文件夹列表已经加载成功<br>![文件夹列表](https://github-share-1304366332.cos.ap-guangzhou.myqcloud.com/art/drawingAndAnimationResources/attachments/img008.png)
8. 你可以任意浏览资料库里面的内容，因为这时候还没有同步任何文件，所以整个库是几乎不会占用你电脑的空间
9. 当你找到想要下载的文件之后，你可以直接双击它进行下载<br>又或者在它上面点击 `右键 > 同步到此设备`<br>![选择并下载文件](https://github-share-1304366332.cos.ap-guangzhou.myqcloud.com/art/drawingAndAnimationResources/attachments/img009.png)
10. 下载完成以后，你可以 `暂停同步` 或 `退出` Sync Home 客户端，待下次需要下载文件时再打开<br>![暂停或退出](https://github-share-1304366332.cos.ap-guangzhou.myqcloud.com/art/drawingAndAnimationResources/attachments/img010.png)

#### 补充说明

+ 不强制要求做贡献！请不要有使用的心理负担，按照自己喜欢的方式使用即可 🥳🥳🥳
+ ⚠ 移动端用户请不要打开 `Use cellular data for sync (使用移动网络进行同步)`，这将会消耗很多流量，因为软件运行时会为其他用户上传文件
+ 文件列表会自动更新，无须反复添加共享文件夹
+ 如果你希望帮助别人，可以选择在不太需要网络的时候开启 Sync Home 客户端，为其他小伙伴提供一点点下载速度
+ 笔记本电脑用户不建议做种，因为 Sync Home 客户端会防止电脑进入休眠状态，而导致电脑会比较烫

## 选择 Resilio Sync 的原因

Resilio Sync 的工作原理类似与 BitTorrent ，也就是大家口中常说的 BT 下载，BT 下载的原理就不再解释了，如果有兴趣大家可以自行 Google 一下

它还支持 Windows Linux Mac Android iOS 等常见的绝大部分的平台

同时，它还能允许用户只同步自己想要的文件，而无须全部文件一次性下载完整

因为它才用 BT 的技术，所以只要有一个用户尚在线，就可以保证文件的存活，当在线的用户越多，后来的下载者就可以获得越快的速度

不过，我并不会强迫大家都来做种，如果大家愿意让这个资料库变得更好的话，可以利用空余时间，挂着 Resilio Sync 的客户端，就算是帮上大忙了

我本人的 NAS 基本上除了夏天气温太高而需要关机以及需要拆机维护以外，基本上 7 × 24h 在线，虽然家里的宽带上传带宽没有太高，但仍可为文件保活，不过却不能保证提供太快的速度

## 软件下载

Windows + Android ：[点此下载](https://github-share-1304366332.cos.ap-guangzhou.myqcloud.com/art/drawingAndAnimationResources/attachments/ResilioSync.zip)

iOS设备请直接在 AppStore 搜索 [Resilio Sync](https://apps.apple.com/app/resilio-sync/id1126282325)

---

[上一级](..)

[笔记首页](/)