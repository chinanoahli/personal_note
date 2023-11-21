---
title: "Android 虚拟机(模拟器)"
date: 2023-11-21T20:20:23+09:00
draft: false
---

# Android 虚拟机(模拟器)

## 支持 Hyper-V 的 Android 虚拟机

大部分 Android 虚拟机都不与 Hyper-V 兼容，但 BlueStacks 可以，下面简述安装步骤

1. 进入国际版 BlueStacks 的[支持页面](https://support.bluestacks.com/hc/en-us)
2. 在搜索栏中输入 `offline` ，然后点击 *Search* 以搜索离线安装包<br>通常最新版为结果的第一个
3. 找到离线安装包的下载页面后，注意描述中是否带有 `Nougat` ，只有带有 `Nougat` 的才是支持 Hyper-V 的版本
4. 用任意 http 下载工具下载你需要的版本 32 / 64 bit
5. 打开 CMD 并使用 `cd` 命令进入到储存 BS 离线安装包的目录
6. 然后运行 <br> `BlueStacksFullInstaller_XXXX_amd64_native.exe --defaultImageName Nougat64 --imageToLaunch Nougat64` <br> 要注意把 `XXXX` 替换成你下载到的版本号，
7. 根据提示完成安装，安装完成后请先退出 BS
8. 打开 *BlueStacks Multi-Instance Manager (BlueStacks 多开管理器) *
9. 点击 *多开管理器* 左下角的 *多开引擎* 按钮，然后选择 *全新多开引擎*
10. 在弹出 *选择 Android 版本* 时，选择你需要的版本，然后点击 *下一步* <br> 如： `安卓11 64位`
11. 根据你的需要选择虚拟机的参数，然后点击右下角的 *下载* 按钮，并等待下载完成
12. 然后在把你下载到的引擎设为默认<br> 按住最右边的 `⇅` 上下箭头按钮并把它拖到最顶端
13. 然后通过 `🗑` 按钮来删除你不需要的版本
14. 使用 *以管理员身份* 来运行主程序即可

---

[上一级](../..)

[笔记首页](/)

