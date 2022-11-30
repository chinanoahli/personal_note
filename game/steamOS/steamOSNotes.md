# SteamOS 使用笔记

## 官方资源快速链接

### 恢复镜像[点此跳转(需要翻墙)](https://help.steampowered.com/zh-cn/faqs/view/1B71-EDF2-EB6D-2BB3)

> 如果无法跳转，请再点一次，此链接似乎会根据IP跳转到不同的页面

Linux dd 快速写盘命令参考

```shell
# 注意要将 /dev/sdX 设成你的USB设备)

bzcat steamdeck-recovery-4.img.bz2 | dd if=/dev/stdin of=/dev/sdX oflag=sync status=progress bs=128M
```

### Windows驱动[点此跳转](https://help.steampowered.com/zh-cn/faqs/view/6121-ECCD-D643-BAA8)

安装顺序(请参考下列文件名)：

1. APU驱动程序<br><sup>APU_XXX.zip</sup>
2. Wi-Fi驱动程序<br><sup>RTLWlanE_XXX.zip</sup>
4. 蓝牙驱动程序<br><sup>RTBlueR_XXX.zip</sup>
5. SD读卡器驱动程序<br><sup>BayHub_SD_STOR_XXX.zip</sup>
6. 音频驱动程序
   + 音频驱动程序1<br><sup>cs35l41_XXX.zip</sup>
   + 音频驱动程序2<br><sup>NAU88L21_XXX.zip</sup>

#### Windows第三方驱动

1. 手柄驱动部分(下列地址均为项目本体GitHub链接，可能需要翻墙)
   + [ViGEmBus](https://github.com/ViGEm/ViGEmBus)<br><sup>专为各种手柄设计的Windows内核驱动</sup>
   + [HidHide](https://github.com/ViGEm/HidHide)<br><sup>对游戏隐藏指定的某个手柄插件</sup>
   + [DS4Windows](https://github.com/Ryochan7/DS4Windows)<br><sup>可以将任意型号的手柄伪装为**PlayStation手柄**或者**Xbox手柄**<br>必须搭配ViGEmBus使用，建议同时用HidHide隐藏自带的手柄</sup>
   + [**S**teamdeck **WI**ndows **C**ontroller **D**river (SWICD)](https://github.com/mKenfenheuer/steam-deck-windows-usermode-driver)<br><sup>第三方手柄驱动<br>\*. 暂时未知是否必须</sup>

## Windows系统游戏体验提升小工具合集

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

   ⚠ 本工具设置上有坑点，请参考[使用攻略](./borderlessGamingUsage.md)，确保读完全文再开始操作

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

## 为*deck*用户设置密码(及取消密码)

```shell
# 设置密码 (输入时不会显示 · 或 *)，根据提示重复输入2次即可
passwd

# 取消密码
passwd -d deck
```

## 如何禁用系统分区的只读属性

```shell
# 需要先为 deck 用户设置密码，请参考上一条

# 禁用
sudo steamos-readonly disable

# 启用
sudo steamos-readonly enable
```

## proton-ge-custom

第三方优化的proton兼容层，**只能**搭配Steam客户端使用

下载地址：[GitHub Releases](https://github.com/GloriousEggroll/proton-ge-custom/releases)

## wine-ge-custom

第三方优化的wine兼容层，建议搭配 **[Lutris](https://lutris.net/)** 使用

下载地址：[GitHub Releases](https://github.com/GloriousEggroll/wine-ge-custom/releases)

### 安装Flathub版的Lutris

```shell
flatpak install flathub net.lutris.Lutris
```

## 初始化pacman包管理器

1. 在 `/etc/pacman.d/mirrorlist` 文件中加入阿里云镜像(放在第一行)

```
Server = https://mirrors.aliyun.com/archlinux/$repo/os/$arch
```

2. 初始化pacman的keyring

```shell
sudo pacman-key --init
```

3. 在keyring中加入默认的密钥

```shell
sudo pacman-key --populate archlinux
```

4. 安装软件包

```shell
sudo pacman -S vim
```

## 安装Steam++(Watt Toolkit)

1. 下载ArchLinux适用的，后缀为`tar.zst`包
2. 使用pacman命令安装该软件包

```shell
# 安装
sudo pacman -U Steam++_linux_x64_v2.8.4.tar.zst

# 移除
sudo pacamn -R Steam++
```

## 为Flathub软件商城添加国内源

[交通大学源](https://mirror.sjtu.edu.cn/docs/flathub)使用方法

```shell
sudo flatpak remote-modify flathub --url=https://mirror.sjtu.edu.cn/flathub
```

如果提示错误，请执行：

```shell
wget https://mirror.sjtu.edu.cn/flathub/flathub.gpg
sudo flatpak remote-modify --gpg-import=flathub.gpg flathub
```

如果中断了某次软件包安装，而导致找不到文件的问题，请用下面的命令修复：

```shell
flatpak repair
```

## 通过Flathub软件商店安装RyujinX或Yuzu模拟器

```shell
# RyujinX
flatpak install flathub org.ryujinx.Ryujinx

# Yuzu
flatpak install flathub org.yuzu_emu.yuzu
```

## 安装/卸载Decky Loader插件管理器

```shell
# 安装稳定版
curl -L https://github.com/SteamDeckHomebrew/decky-loader/raw/main/dist/install_release.sh | sh

# 安装预发布(或称预览版、测试版)
curl -L https://github.com/SteamDeckHomebrew/decky-loader/raw/main/dist/install_prerelease.sh | sh

# 卸载
curl -L https://github.com/SteamDeckHomebrew/decky-loader/raw/main/dist/uninstall.sh | sh

# 翻墙问题自理
```

完全手动安装，请参考[安装脚本](https://github.com/SteamDeckHomebrew/decky-loader/blob/main/dist/install_release.sh)，安装脚本很短，有经验的Linux使用者应该可以完全读懂

---

[上一级](../README.md)

[笔记首页](../../README.md)
