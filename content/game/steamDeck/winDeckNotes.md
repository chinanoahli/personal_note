---
title: "Windows on Deck 使用笔记"
date: 2023-05-05T19:21:53+09:00
draft: false
---

# Windows on Deck 使用笔记

> 本篇只涉及 Windows on Deck 的使用
>
> 如果需要在 Steam Deck 上使用 SteamOS 的相关信息，请[点击这里](../steamOSNotes)

## 官方资源快速链接

### Windows驱动[点此跳转](https://help.steampowered.com/zh-cn/faqs/view/6121-ECCD-D643-BAA8)

安装顺序(请参考下列文件名)：

1. APU驱动程序<br><sup>APU_XXX.zip<br>Aerith Windows Driver_XXX.zip</sup>
2. Wi-Fi驱动程序<br><sup>RTLWlanE_XXX.zip</sup>
4. 蓝牙驱动程序<br><sup>RTBlueR_XXX.zip</sup>
5. SD读卡器驱动程序<br><sup>BayHub_SD_STOR_XXX.zip</sup>
6. 音频驱动程序
   + 音频驱动程序1<br><sup>cs35l41_XXX.zip</sup>
   + 音频驱动程序2<br><sup>NAU88L21_XXX.zip</sup>

### Windows第三方驱动

1. 手柄驱动部分(下列地址均为项目本体GitHub链接，可能需要翻墙)
   + [ViGEmBus](https://github.com/ViGEm/ViGEmBus)<br><sup>专为各种手柄设计的Windows内核驱动</sup>
   + [HidHide](https://github.com/ViGEm/HidHide)<br><sup>对游戏隐藏指定的某个手柄插件</sup>
   + [DS4Windows](https://github.com/Ryochan7/DS4Windows)<br><sup>可以将任意型号的手柄伪装为**PlayStation手柄**或者**Xbox手柄**<br>必须搭配ViGEmBus使用，建议同时用HidHide隐藏自带的手柄</sup>
   + [**S**teamdeck **WI**ndows **C**ontroller **D**river (SWICD)](https://github.com/mKenfenheuer/steam-deck-windows-usermode-driver)<br><sup>第三方手柄驱动<br>\*. 暂时未知是否必须</sup>

### Windows系统游戏体验提升小工具合集

1. Borderless Gaming

   > 功能简介:
   >
   > 1. 以无边框方式启动软件
   > 2. 置顶任何窗口(不受全屏游戏影响)
   > 3. 设置窗口显示位置
   > 4. 设置窗口大小
   > 5. 使鼠标光标不可见
   > 6. 使任务栏不可见

   [Steam有售(赞助开发者)](http://store.steampowered.com/app/388080)，亦可在[GitHub](https://github.com/Codeusa/Borderless-Gaming)直接下载，软件开源免费

   ⚠ 本工具设置上有坑点，请参考[使用攻略](../borderlessGamingUsage)，确保读完全文再开始操作

3. Winformation

   > 功能简介:
   >
   > 1. 将任意窗口设置为半透明显示
   > 2. 置顶任何窗口(不受全屏游戏影响)
   > 3. 设置窗口显示位置
   > 4. 设置窗口大小

   下载地址: [52pojie](https://www.52pojie.cn/thread-1416482-1-1.html)，免费但不开源

2. WindowTop (虽然是集大成者，但却不推荐使用)

   可以将任意窗口置顶(且不受全屏游戏的影响)并设置透明度显示，提升系统自带屏幕键盘体验

   上述两个功能无需购买激活码(也不建议买)，直接使用免费版即可

   ⚠ 软件有挺多bug，而且运行效率感人 ⚠

   为系统自带的屏幕键盘设置屏幕置顶时，需要**以管理员身份运行**该软件

   在设置窗口置顶时，不建议打开窗口边框颜色选项，因为有拖动窗口后，边框还停留在原本的位置的情况

   下载地址：[GitHub Releases](https://windowtop.info/)，部分功能收费且不开源

---

[上一级](../..)

[笔记首页](/)
