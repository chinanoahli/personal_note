# MacOS 使用技巧

> 收录一些MacOS系统目前遇到过的问题的解决方案。

> **sudo** 要求输入管理员帐号的密码，输入密码时不会显示 **∙** 或 **\***，确保输入无误后按 **enter/return** 即可。

---

## 禁用 *「App」尚未针对您的Mac优化* 提示

打开 *Terminal* 根据需要运行以下命令

命令作用|命令|测试环境
----|----|----
**禁用**最佳化提示|`defaults write -g CSUIDisable32BitWarning -boolean TRUE`|MacOS 10.14.6 (18G84) 通过
*启用*最佳化提示|`defaults delete -g CSUIDisable32BitWarning`|未测试
查看当前设置|`defaults read -g CSUIDisable32BitWarning`|未测试

![示例图像](https://github-share-1304366332.cos.ap-guangzhou.myqcloud.com/softUsage/operatingSystem/macOS/img001.jfif)

#### 来源：
1. [Apple官方介绍页面](https://support.apple.com/zh-cn/HT208436)
2. [How to suppress alert 'this app is not optimized for your Mac'](https://apple.stackexchange.com/questions/324139/how-to-suppress-alert-this-app-is-not-optimized-for-your-mac)

---

## 修改 hostname

本技巧可以在你的计算机名(Hostname)加入非英文字符。
> 至于在不同网络环境和不同系统通讯的情况下，非英文字符的兼容性还请自行测试。

打开 *Terminal* 根据需要运行以下命令

```shell
sudo scutil --set ComputerName 计算机名
sudo scutil --set HostName 计算机名
```

---

## 修改 Dock 图标大小

本技巧可以使强迫症患者不再需要跟无法量化的水平调节器打交道。

打开 *Terminal* 根据需要运行以下命令

```shell
defaults write com.apple.dock largesize -float 88  # 鼠标经过(放大)时图标的大小
defaults write com.apple.dock tilesize -int 48     # 普通情况下图标的大小
killall Dock                                       # 设置完要重启一下Dock才能生效
```

---

## 解包 PKG 文件

使用前请在PKG包上右键看看有没有*显示包内容*选项，如果有，证明这个安装包并非单文件，而是文件夹，直接点击*显示包内容*即可查看内容。
> PKG指的是PKG格式的MacOS软件包安装文件，并非所有PKG都能使用此技巧！

打开 *Terminal* 根据需要运行以下命令

```shell
cd path/to/pkg/file
pkgutil --expand ExampleApp.pkg  ExampleApp.unpkg  # 解包PKG 10.12及之前的系统解包目标路径一定要加上`.unpkg`否则会解包失败
pkgutil --flatten ExampleApp.unpkg ExampleApp.pkg  # 打包PKG (未测试)

# 解包后请在解包出来的目录中寻找 Payload 文件，此文件包含真正的应用文件。

cd path/to/Payload/file
cat Payload | gzip -d | cpio -id                   # 解包出真正的应用文件
```

---

## 打开/关闭 [*SIP*](https://support.apple.com/zh-cn/HT204899) 安全机制(高危操作)

> 本操作可能导致系统不可逆损坏，请在执行前确保你清楚自己正在干什么！！

使用此方法需要先将Mac关机，然后按住 `Command + R`开机，请一直按着`CMD + R`直到完全进入「[恢复功能](https://support.apple.com/zh-cn/HT201314)」模式。

在「恢复功能」模式下打开 *Terminal* 根据需要运行以下命令

```shell
csrutil disable  # 禁用SIP
csrutil enable   # 启用SIP
csrutil clear    # 重置SIP (默认值为启用)
csrutil status   # 查看SIP设置 (可在正常系统下使用本命令)
```

---

## 在「[恢复功能](https://support.apple.com/zh-cn/HT201314)」模式下修复全盘文件权限错误

> 此方法**仅**适用于**尚未**应用 [*SIP*](https://support.apple.com/zh-cn/HT204899) 安全机制的系统(OS X El Capitan以前的系统，不包括OS X El Capitan)，相关命令行工具在包含SIP的系统上已经被苹果**移除**！因此强烈**不**建议在日常使用中长时间关闭SIP保护！

使用此方法需要先将Mac关机，然后按住 `Command + R`开机，请一直按着`CMD + R`直到完全进入「恢复功能」模式。

在「恢复功能」模式下打开 *Terminal* 根据需要运行以下命令，假设你的系统盘盘符为「Macintosh HD」

```shell
sudo /usr/libexec/repair_packages --verify --standard-pkgs /Volumes/Macintosh\ HD/
                                                                    ^ 改成你系统盘的名称
sudo /usr/libexec/repair_packages --repair --standard-pkgs --volume /Volumes/Macintosh\ HD/
                                                                             ^ 改成你系统盘的名称
```

---

## 通过*Terminal*打开「所有来源」
#### (允许从以下来源下载的App)

打开 *Terminal* 根据需要运行以下命令

命令作用|命令
----|----
**打开**「所有来源」|`sudo spctl --master-disable`
*关闭*「所有来源」|`sudo spctl --master-enable`

---

## 手动删除出错的升级安装包
#### (包括系统更新/AppStore应用更新)

有时在更新过程中，因为网络或各种各样的问题导致安装包下载过程中出现错误，且出错后无法继续下载或下载完成后无法安装等情况，此时只需要将出错的安装包文件删除并重新下载即可。

升级安装包路径，删除里面的所有文件，只保留*ProductMetadata.plist*文件即可

打开 *Terminal* 根据需要运行以下命令可直接打开升级包所在的目录

```shell
open /Library/Updates/
```

---

## 查看/修改默认XCode的路径

MacOS系统中只能同时指定一个XCode作为开发工具，如果有多个不同版本的XCode需要手动切换。

打开 *Terminal* 根据需要运行以下命令

命令作用|命令
----|----
*查看*当前启用的Xcode路径|`xcode-select --print-path`
**修改**当前启用的Xcode路径|`sudo xcode-select -switch path/to/Xcode.app`
**安装**XCode*命令行工具*|`sudo xcode-select --install`

---

## iBooks数据目录

打开 *Terminal* 根据需要运行以下命令可直接打开iBook数据目录

```shell
open ~/Library/Containers/com.apple.BKAgentService/Data/Documents/iBooks/Books
```

---

## 重建「打开方式」菜单

打开 *Terminal* 根据需要运行以下命令

```shell
/System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/LaunchServices.framework/Versions/A/Support/lsregister -kill -r -domain local -domain user
```

#### 来源：
1. [如何搜索适用于您的文件的应用](https://support.apple.com/zh-cn/HT201290)

---

## 修改Dock文件夹显示的图标大小

先点击在Dock中停靠的任意文件夹，使其弹出内容显示框，然后根据需要按下下面的组合键进行调整

```shell
Command =  # 放大图标显示 Command键 加 = (shift 是 + 那个 =)
Command -  # 缩小图标显示 Command键 加 - (shift 是 _ 那个 -)
```

> 在一些文本编辑应用中你也可以尝试使用这组快捷键来调整字体大小。

---

## 修改系统登录/锁屏界面的背景图片
#### (去除模糊效果，仅适用于10.12之前的系统)

使用喜欢的图片替换以下文件即可

```shell
/Library/Caches/com.apple.desktop.admin.png
```

---

## 去除文件「@」特殊属性

> 在HFS+文件系统里，本操作可能使软连接失效，使用时请注意。

MacOS的Finder可以给文件或文件夹加上颜色标签，此功能需要创建一个名为`._原文件名`的文件，在MacOS上表现为通过终端列出此文件会带有特殊的「@」属性。
在可移动存储媒体里面，这些属性如果在别的系统中表现出来会非常杂乱。但可以通过命令方便地去除这些属性。

打开 *Terminal* 根据需要运行以下命令

```shell
xattr -rc 文件名/文件夹名
```

使用示例：

```shell
bash-5.0$ ls -ahl
-rw-r--r--@  1 user  staff     0B Aug  3 11:40 NewFile.txt

          ^ 「@」属性标记，以上为实验性地为一个文件加上颜色标签后的结果。

bash-5.0$ xattr -rc NewFile.txt  # 通过 xattr -rc 文件名/文件夹名 可以递归地删除文件/文件夹里面所有文件的「@」属性标记。

bash-5.0$ ls -ahl
-rw-r--r--   1 user  staff     0B Aug  3 11:40 NewFile.txt

          ^ 执行后「@」属性标记消失。
```

---

## 创建 MacOS 的安装媒体
#### (适用于 OS X 10.10 及以上系统)

> 本操作会对U盘**重新分区**，请提前备份U盘内容！

从 App Store 下载最新的系统安装程序。
提前准备一只容量最小为 8G 的U盘并格式化，卷标（盘符名称）随意(此处以`Untitled`作为示例)。

打开 *Terminal* 根据需要运行以下命令

```shell
sudo "path/to/Installer.app/Contents/Resources/createinstallmedia" --volume /Volumes/Untitled --applicationpath "path/to/Installer.app/Contents/Resources/createinstallmedia" --nointeraction
                                                                                     ^ 改成你U盘的卷标
```

#### 来源：
1. [How to make a bootable OS X 10.10 Yosemite install drive](http://www.macworld.com/article/2367748/how-to-make-a-bootable-os-x-10-10-yosemite-install-drive.html)

---

## 重建 Launchpad 数据库
#### (适用于 OS X 10.10 及以上系统)

> 本操作会重置Launchpad，所有系统应用的图标都会回到系统**默认**的位置，而自己安装的应用则会**随机**排列到第二页及以后的位置。

本操作可以解决Launchpad里面还残留了已经删除的App图标，或者出现图标错位，删除不了的情况。

打开 *Terminal* 根据需要运行以下命令

```shell
defaults write com.apple.dock ResetLaunchPad -bool true
killall Dock
```

![示例图像](https://github-share-1304366332.cos.ap-guangzhou.myqcloud.com/softUsage/operatingSystem/macOS/img002.jfif)

#### 来源：
1. [How to Rebuild Launchpad Database in OS X Yosemite (10.10) and Later](https://mariusvw.com/2017/10/21/how-to-rebuild-launchpad-database-in-os-x-yosemite-10-10-and-later/)

---

## 优雅地在MacOS中隐藏文件

本操作利用MacOS的「[@](#user-content-去除文件特殊属性)」属性隐藏，而非Unix标准的将文件名或文件夹名改成`.`开头的办法。

利用本操作可以隐藏`/Applications`中的系统应用，而不对系统造成损害或破坏性修改。

> 在**MacOS 10.14**及以后系统中，一部分系统应用已经以至`/System/Applications`目录下。

（启用了[*SIP*](https://support.apple.com/zh-cn/HT204899)的系统，若要修改`/Applications`中的系统应用，请到「[恢复功能](https://support.apple.com/zh-cn/HT201314)」模式下使用本命令；或先行关闭SIP，修改完毕后再重新打开SIP）

打开 *Terminal* 根据需要运行以下命令

命令作用|命令
----|----
**隐藏**文件 / 文件夹|`chflags hidden 文件/文件夹`
取消隐藏|`chflags nohidden  文件/文件夹`

---

## 修改锁屏或开机登入用户账户时的背景图片
#### (适用于 MacOS 10.15 及以上系统，其他版本尚未出现此情况)

本操作可以修复因误操作，设置了错误或不适宜的图片作为桌面背景后被系统记录，导致每次登入用户账户在输入密码的步骤都显示该图片作为背景图片的情况。

删除以下路径的图片即可
```shell
/Library/Caches/Desktop Pictures/89EE1E2D-C40A-40B6-A7F0-F7C3DCF2EB41/lockscreen.png
                                 ^ 此为用户账户UUID，可以在下面的位置进行查询
                                   系统偏好设置 > 用户与群组 > 解锁 > 在用户账户上单击鼠标右键 > 进阶选项
```

---

## 在日历应用中订阅苹果官方节庆日历

![示例图像](https://github-share-1304366332.cos.ap-guangzhou.myqcloud.com/softUsage/operatingSystem/macOS/img003.jfif)

1. 在“日历”中，选取“文件”>“新建日历订阅”。

2. 输入日历的网址，然后点按“订阅”。

3. 输入日历名称，然后选取一种颜色来帮助您在日历上标识这个名称。

  + 若为苹果官方提供的日历，则可以自动识别日历名称，如`日本の祝日`等

4. 从“位置”菜单中选取“iCloud”，然后点按“好”。

  + 若不需要iCloud同步，这里可以选“我的Mac上”

```
日本节假日 https://p33-calendars.icloud.com/holidays/jp_ja.ics
大陆节假日 https://p48-calendars.icloud.com/holidays/cn_zh.ics
台湾节假日 https://p48-calendars.icloud.com/holidays/tw_zh.ics
香港节假日 https://p48-calendars.icloud.com/holidays/hk_zh.ics
美国节假日 https://p62-calendars.icloud.com/holidays/us_en.ics
```

#### 来源：

1. 苹果支持知识库编号[HT202361](https://support.apple.com/zh-cn/HT202361)

---

## 禁止某个分区自动挂载

> 本操作可以禁止任意分区（可以是任意文件系统，如：NTFS、HFS+等）在系统开机、重启、或拔出USB硬盘后重新连接时自动挂载

1. 先打开 *Terminal* 运行以下命令。<br/>并记录你需要禁止自动挂载的分区的**IDENTIFIER**。<br/>本文以笔者系统中的`Windows_BC`分区为例，所以在本例中应该记录的是`disk0s3`

  ```shell
  $ diskutil list    # 显示目前连接在电脑上的硬盘信息

  # 以下是在 macOS 10.15 中的输出示例

  /dev/disk0 (internal, physical):
     #:                       TYPE NAME                    SIZE       IDENTIFIER
     0:      GUID_partition_scheme                        *500.3 GB   disk0
     1:                        EFI EFI                     209.7 MB   disk0s1
     2:                 Apple_APFS Container disk1         460.0 GB   disk0s2
     3:       Microsoft Basic Data Windows_BC              40.1 GB    disk0s3

  /dev/disk1 (synthesized):
     #:                       TYPE NAME                    SIZE       IDENTIFIER
     0:      APFS Container Scheme -                      +460.0 GB   disk1
                                   Physical Store disk0s2
     1:                APFS Volume Macintosh HD - 資料     288.3 GB   disk1s1
     2:                APFS Volume Preboot                 83.4 MB    disk1s2
     3:                APFS Volume Recovery                528.1 MB   disk1s3
     4:                APFS Volume VM                      10.7 GB    disk1s4
     5:                APFS Volume Macintosh HD            11.2 GB    disk1s5
  ```

2. 继续在 *Terminal* 运行以下命令，即可得出该分区的详细信息。<br/>记录下该分区的**Volume UUID**，所以在本例中应该记录的是`4C31E7AC-26AD-4347-8139-C3DFCEC13DBB`

  ```shell
  $ diskutil info /dev/disk0s3    # 请将例子中的`disk0s3`换成你实际要操作的`IDENTIFIER`

  # 在我系统中的示例输出，
  Device Identifier:         disk0s3
  Device Node:               /dev/disk0s3
  Whole:                     No
  Part of Whole:             disk0

  Volume Name:               Windows_BC
  Mounted:                   No

  Partition Type:            Microsoft Basic Data
  File System Personality:   NTFS
  Type (Bundle):             ntfs
  Name (User Visible):       Windows NT File System (NTFS)

  OS Can Be Installed:       No
  Media Type:                Generic
  Protocol:                  PCI
  SMART Status:              Verified
  Volume UUID:               4C31E7AC-26AD-4347-8139-C3DFCEC13DBB
  Disk / Partition UUID:     87B2CB4F-5A5A-46FC-8EF9-5DC36D618B4B
  Partition Offset:          460210569216 Bytes (898848768 512-Byte-Device-Blocks)
  # 省略一部分输出内容
  ```

3. 继续在 *Terminal* 运行以下命令，并在打开的**nano**编辑器显示的文件最末尾增加一行（**请勿**删除或修改已经存在的任何内容），内容如下所示：

  ```
  $ export EDITOR=nano    # 指定shell编辑器为nano
                          # 如果你安装了自己喜欢的编辑器，也可以改成你自己喜欢的编辑器，如 vim

  $ sudo vifs
  Password:               # 输入管理员密码然后回车

  # 在文件末尾增加以下内容，请将UUID换成你记录下的UUID
  UUID=4C31E7AC-26AD-4347-8139-C3DFCEC13DBB none auto noauto,ro

  # 如果你使用的是nano编辑器，请按以下步骤保存并退出文件编辑状态
  编辑完成后按 control + x (退出编辑器)
  最后再键入 Y (保存修改)
  ```

4. 此时已禁止系统对选定的分区进行自动挂载，如果需要取消禁止，可以重复**第3步**，删除对应的**UUID**所在的行即可

> **Volume UUID**是在分区格式化时由系统自动生成的，此后直到下一次格式化为止一般不再改变。<br/>假如你禁用某分区自动挂载后，又对其进行了格式化操作，可能需要按照以上步骤重新禁用。

---

[上一级](../README.md)

[笔记首页](../../../README.md)
