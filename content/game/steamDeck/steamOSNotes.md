---
title: "SteamOS 使用笔记"
date: 2023-05-05T19:21:42+09:00
draft: false
---

# SteamOS 使用笔记

> 本篇只涉及 SteamOS (ArchLinux) 的使用
>
> 如果需要在 Steam Deck 上使用 Windows 的相关信息，请[点击这里](../winDeckNotes)

## 首次开机无法更新

> 这个方法可以解决更新卡 `正在安装 / Installing` 或 `剩余1秒 / 1 second remaining`
>
> 需要一个 *USB HUB* 用于插入外置键盘
>
> 引用来源: [Reddit帖子](https://www.reddit.com/r/SteamDeck/comments/t4x2q6/comment/iucl33j/?utm_source=share&utm_medium=web2x&context=3)

1. 在进入首次开机设置后，先根据提示连接互联网，Wi-Fi 或 有线网络 均可

   ⚠注意⚠：成功联网即可，千万不要点击下一步

2. 同时按下键盘的 `Ctrl + Alt + F4`，进入 **tty** 模式

3. 使用用户 `deck` 登录，默认无密码

4. `passwd` 更改 `deck` 用户的密码 (参考后面 **设置密码** 的部分)

5. 运行命令 `sudo steamos-update`，并根据提示输入刚才设置的密码

   如果有可用的更新，系统将会提示 `Update available` 并自动下载

   安装完成后会显示 `Applied an update`

6. 运行命令 `sudo reboot` 重启Deck，即可更新成功

## 官方资源快速链接

### 恢复镜像[点此跳转(需要翻墙)](https://help.steampowered.com/zh-cn/faqs/view/1B71-EDF2-EB6D-2BB3)

> 如果无法跳转，请再点一次，此链接似乎会根据IP跳转到不同的页面

Linux dd 快速写盘命令参考

```shell
# 注意要将 /dev/sdX 设成你的USB设备)

bzcat steamdeck-recovery-4.img.bz2 | dd if=/dev/stdin of=/dev/sdX oflag=sync status=progress bs=128M
```

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

下载地址: [GitHub Releases](https://github.com/GloriousEggroll/proton-ge-custom/releases)

手动安装方法:

1. 运行命令 `mkdir -p ~/.steam/root/compatibilitytools.d` 创建安装路径

2. 运行命令 `tar -xf GE-ProtonX-XX.tar.gz -C ~/.steam/root/compatibilitytools.d/` 将 `GE-Proton` 解压到对应目录

3. 重启Steam客户端，或重启机器

4. 在Steam客户端中，调整游戏参数，手动选择 `GE-Proton`

## wine-ge-custom

> 第一次打开 Lutris 会遇到网络问题，目前还没找到解决办法，留个坑日后更新

第三方优化的wine兼容层，建议搭配 **[Lutris](https://lutris.net/)** 使用

下载地址: [GitHub Releases](https://github.com/GloriousEggroll/wine-ge-custom/releases)

手动安装方法:

1. 运行命令 `mkdir -p ~/.local/share/lutris/runners/wine` 创建安装路径

2. 运行命令 `tar -xf wine-name-branch-x86_64.tar.gz -C ~/.local/share/lutris/runners/wine` 将 `wine-ge-custom` 解压到对应目录

3. 在Lutris客户端中，调整游戏参数，选择以 `wine-name-branch-x86_64` 作为 Runner

### 安装Flathub版的Lutris

```shell
flatpak install flathub net.lutris.Lutris
```

## 初始化pacman包管理器

> 不要使用第三方源（如阿里云和腾讯云等原版 ArchLinux 的源镜像），会有不匹配的情况

1. 初始化pacman的keyring

```shell
sudo pacman-key --init
```

2. 在keyring中加入默认的密钥

```shell
sudo pacman-key --populate archlinux
```

3. 更新软件包缓存并安装软件包

```shell
sudo pacman -Syy vim
```

## 安装Steam++(Watt Toolkit)

> 到 2023-Jan-22 为止，该官方包仍存在问题，无法直接通过 `pacman` 命令安装
>
> 安装时会提示 `missing package metadata` 错误

1. 下载ArchLinux适用的，后缀为`tar.zst`包

2. 使用pacman命令安装该软件包

```shell
# 安装
sudo pacman -U Steam++_linux_x64_vX.X.X.tar.zst

# 移除
sudo pacamn -R Steam++
```

## 为Flathub软件商城添加国内源 (交大源已经与Flathub官方合并，换了还是慢，时快时慢)

[交通大学源](https://mirror.sjtu.edu.cn/docs/flathub)使用方法

> 这里的操作不会覆盖官方源，如果你已经覆盖过官方源，且希望恢复官方源，你可以运行以下命令
>
>> `sudo flatpak remote-modify flathub --url=https://flathub.org/repo/flathub.flatpakrepo`
>
> 或在图形界面中，先删除所有源，然后运行下列命令，完成后，继续操作本节内容即可
>
>> `sudo flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo`

```shell
# 添加源
sudo flatpak remote-add --if-not-exists sjtu https://mirror.sjtu.edu.cn/flathub
# 下载源服务器公钥
wget https://mirror.sjtu.edu.cn/flathub/flathub.gpg
# 导入源服务器公钥
sudo flatpak remote-modify --gpg-import=flathub.gpg sjtu
```

如果中断了某次软件包安装，而导致找不到文件的问题，请用下面的命令修复:

```shell
flatpak repair
```

## 通过Flathub软件商店安装RyujinX或Yuzu模拟器

> 不推荐时候用Flathub安装，因为实在太慢了，建议使用 [EmuDeck](https://github.com/EmuDeck/emudeck-electron/releases)
>
> Ryujinx 需要的配置很高，Deck上体验较差，可以只选用Yuzu

```shell
# Ryujinx
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

## 找回消失的 `Return to Gaming Mode`

SteamOS 在 桌面模式 的桌面会有一个图标，让玩家可以立即退出桌面模式并回到游戏模式，但是因为某些原因，这个图标偶尔会被莫名其妙地删除掉

这时只需要在桌面新建一个文件名为 `Return.desktop` 的文件(注意后缀应该为 `.desktop` )，内容为下面的内容，即可找回该功能

```text
[Desktop Entry]
Name=Return to Gaming Mode
Exec=qdbus org.kde.Shutdown /Shutdown org.kde.Shutdown.logout
Icon=steamdeck-gaming-return
Terminal=false
Type=Application
StartupNotify=false
```

## SteamOS 默认设置调优

> 本节内容针对有经验的 Linux 用户，不作详细操作解释
>
> 引用来源:
>
> 1. [第 1～3 项](https://github.com/csrutil/steamdeck/tree/draft)

1. 优化日志文件的占用空间

   在默认情况下 Steam OS 并未对系统日志的大小作出限制，对于游戏掌机，系统日志的作用不大

   所以我们可以设置一个小一点的限制，以防日志占用太多空间

   调整方法:

   将 `/etc/systemd/journald.conf` 文件里面 `[Journal]` 段落的 `SystemMaxUse` 参数改为 `SystemMaxUse=50M`

   然后重启系统日志守卫进程: `systemctl restart systemd-journald`

2. 调整 Swap 的使用策略

   SteamOS 默认的 Swap 使用策略是`积极使用Swap`，这意味着系统在内存负载不高的情况下，也可能会产生大量磁盘I/O

   在这里我们可以选择将 Swap 使用策略调整为最大限度地使用物理内存，以减轻这种情况

   调整方法:

      1. 将 `/etc/sysctl.d/swappiness.conf` 文件里面的 `vm.swappiness=100` 改为 `vm.swappiness=0`

      2. 然后重启系统

3. 关闭 CPU 熔断/幽灵漏洞的微码补丁

   > 在这里不扛安全性问题，掌机基本除了玩游戏不干其他事，基本绝大部分时间可以算为安全范畴

   众所周知，熔断/幽灵补丁会降低 CPU 的性能，所以在这里我们可以把该补丁禁用掉，让 CPU 回到真正的能力水平

   调整方法:

      1. 修改 `/etc/default/grub` 文件里面的 `GRUB_CMDLINE_LINUX_DEFAULT` 参数，在该参数的最后面加上 `mitigations=off`

      2. 更新Grub，应用新的启动参数 `update-grub`

      3. 重启系统

   查询方法:

      运行 `lscpu`  命令

      > 如果打开了该补丁，会有类似的输出 (输出中带有`Mitigation`)
      >
      > ```text
      > Vulnerabilities:
      > Spec store bypass:     Mitigation; Speculative Store Bypass disabled via prctl and seccomp
      > Spectre v1:            Mitigation; usercopy/swapgs barriers and __user pointer sanitization
      > Spectre v2:            Mitigation; Full AMD retpoline, IBPB conditional, IBRS_FW, STIBP conditional, RSB filling
      > ```
      >
      > 如果关闭了该补丁，会有类似的输出 (输出中带有`Vulnerable`)
      >
      > ```text
      > Vulnerabilities:
      > Spec store bypass:     Vulnerable
      > Spectre v1:            Vulnerable: __user pointer sanitization and usercopy barriers only; no swapgs barriers
      > Spectre v2:            Vulnerable, IBPB: disabled, STIBP: disabled
      > ```

---

[上一级](../..)

[笔记首页](/)
