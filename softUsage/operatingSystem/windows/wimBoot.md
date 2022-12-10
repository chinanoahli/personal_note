# 从Wim映像文件中启动Windows

> 这里只简述步骤，具体原理可能以后补充，也可能不会补充
>
> 如需要了解原理，请参考[Windows Image File Boot (WimBoot)](https://learn.microsoft.com/en-us/windows/win32/w8cookbook/windows-image-file-boot--wimboot-)
>
> 若此链接失效，请直接在[Microsoft Lean](https://learn.microsoft.com/en-us/)中搜索`wimboot`即可

> 这里的例子会将Wim映像文件单独放到一个分区中，这个分区会被设置为恢复分区，默认情况下，不会显示在 *Explorer* 中

## 准备用于WimBoot的映像文件

默认情况下，微软提供的安装光盘中的系统映像是不可以直接用于WimBoot的

我们需要先从安装光盘中找到 `X:\sources\install.wim` 文件，并将它复制到任意可读写的路径中

然后在控制台中利用 **<i>Dism</i>** 命令将需要的映像导出为可以WimBoot的映像，注意，按需选择对应的 *Index* 即可

```shell
Dism /Export-Image /SourceImageFile:\SourceWIMFilePath.wim /SourceIndex:1 /DestinationImageFile:\DestinationWIMFilePath.wim
```

在导出对应的映像之后，推荐进行以下的操作（非必须）：

+ 移除系统自带的 *WinRE* 环境，以减小映像文件体积<br>对应的文件在 `MountPoint\Windows\Windows\System32\Recovery\winre.wim`
+ 按需加入语言包、.Net3.5、IE、补丁等
+ 对映像进行清理并最佳化，以减小映像文件体积<br>参见[DISM命令速查](./dismCommands.md)

得到基本映像之后，我们还需要给加入WimBoot支持

```shell
Dism /Export-Image /WIMBoot /SourceImageFile:\SourceWIMFilePath.wim /SourceIndex:1 /DestinationImageFile:\DestinationWIMFilePath.wim
```

准备好映像之后，我们可以通过以下的命令对映像进行检查

```shell
Dism /Get-ImageInfo /ImageFile:\WIMFile.wim /Index:1
```

若正确无误，返回中应包含 `WIM Bootable : Yes` 字段

## 准备系统安装磁盘

接下来通过 *WinPE*  启动电脑，这里推荐使用系统安装光盘自带的PE或者[Windows ADK](https://learn.microsoft.com/en-us/windows-hardware/get-started/adk-install)提供的PE

在我试验时，我一开始使用的是USM，但是USM把命令行工具 `diskpart` 精简掉了，导致无法继续操作

进入PE后按  `Shift + F10` 调出控制台，然后利用 `diskpart` 命令为硬盘分区

```shell
diskpart

:: 根据自己的系统环境选择硬盘号，并重建GPT分区表
select disk X
clean
convert gpt

:: 创建一个 300M 的 EFI 分区
create partition efi size=300
format quick fs=fat32 label=EFI

:: 将剩余的空间都分配给主分区，用作系统盘
create partition primary

:: 缩减系统盘空间，在磁盘最后面保留8G空间
shrink minimum=8192

:: 格式化系统盘，将卷标设为`OS`，并为其指派盘符`C`
format quick fs=ntfs label=OS
assign letter=c

:: 利用保留的8G空间创建专门用于存放映像文件的分区
:: 格式化分区，将卷标设为`WimImgs`，并指为其派盘符`M`
:: 这里不推荐将盘符指派成`D`和`E`，因为PE启动时很可能光驱已经占用了这些盘符
:: 挑选一个在字母表中后的字母较为稳妥
create partition primary
format quick fs=ntfs label=WimImgs
assign letter=m

:: 调整映像分区的参数，让它成为不可见的恢复分区
set id="de94bba4-06d1-4d40-a16a-bfd50179d6ac"
gpt attributes=0x8000000000000001
::                ^ 14个0

:: 退出 diskpart
exit
```

## 进行WimBoot的安装和引导程序设置

在准备好硬盘的分区之后，接下来我们需要把映像复制到已经准备好的磁盘中

> 安装光盘自带的安装程序并不适用与设置WimBoot，所以不能直接使用安装光盘提供的GUI安装程序

首先我们需要将准备好的映像文件复制到储存映像的盘中，在本例就是M盘

```shell
Copy WIMFile.wim M:\
```

接下来，需要以WimBoot方式释放文件（即创建文件指针）

```shell
Dism /Apply-Image /ImageFile:M:\WIMFile.wim /ApplyDir:C: /Index:1 /WIMBoot
```

最后，我们还需要手动写入BCD引导程序

```shell
C:\Windows\System32\bcdboot.exe C:\Windows /L zh-cn "Windows 10 (WimBoot)"
```

到这里，全部操作已经完成，只需要重启即可进入系统准备阶段

## 验证安装正确性

为了验证系统是否以WimBoot的方式安装，你可以尝试以下步骤：

+ 以管理员身份运行 `fsutil wim enumwims C:` 并查看返回信息
+ 在 *磁盘管理器* 中查看系统盘是否包含 `Wim 引导` 参数

## 如何快速重装

首先当然还是把电脑启动到PE环境并调出控制台

接着需要利用 `diskpart` 将C盘格式化

```shell
diskpart

:: 根据自己的系统环境选择硬盘号
select disk X

:: 列出硬盘里的所有分区
list volume

:: 根据自己的系统环境，选择C盘对应的磁盘号
select volume X

:: 格式化系统盘，将卷标设为`OS`
format quick fs=ntfs label=OS

:: 现在还无需退出 diskpart !!
```

到此，我们还需要将恢复分区手动挂载一下，因为恢复分区是不会被系统自动分配盘符的

```shell
:: 在上面列出分区的步骤，应该可以看到我们存放映像文件的恢复分区了
:: 这里为恢复分区分配盘符`M`，以便我们可以访问它里面的映像文件
select volume Y
assign letter=m

:: 退出 diskpart
exit
```

然后重新运行一下Dism命令，以WimBoot的方式释放系统文件到C盘即可

```shell
Dism /Apply-Image /ImageFile:M:\WIMFile.wim /ApplyDir:C: /Index:1 /WIMBoot
```

注意，这里我们无需重新写入BCD引导程序

因为BCD引导程序是存放在EFI分区，而不是系统盘C盘里面的，所以并不会被重装过程影响到

到这里重装就结束了，我们只需要重启电脑即可进入系统准备阶段

---

[上一级](../README.md)

[笔记首页](../../../README.md)