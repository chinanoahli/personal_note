---
title: "Windows 常用技巧"
date: 2023-05-05T19:53:27+09:00
draft: false
---

# Windows 常用技巧

## 修复文件或路径无权访问的情况

我曾经在我电脑上用两个不同的硬盘安装了相同版本的 Windows 10 系统，并且使用了一个相同的用户名 `chinanoahli`

但是不久后，我发现，每次当我换不同的硬盘启动时，系统完成用户账户登录并进入桌面后，总会提示 **某分区的回收站损坏**

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

```
Do you want to allow your PC to be discoverable by other PCs and devices on this network?

We recommend allowing this on your home and work networks, but not public ones.
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
"RealTimeUniversal"=dword:00000001
```

## 自动卸载在内存中的DLL

**DLL** 是Windows系统的动态链接库文件，在一般情况下，Windows不会主动卸载已经装载在内存中的DLL

你可以通过新增下面的注册表值来强制Windows自动卸载当前没有被程序调用的DLL

```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer]
"AlwaysUnloadDLL"=dword:00000001
```

## 禁用幽灵\&熔断漏洞的微码补丁

众所周知，禁用这两个漏洞的补丁，会导致安全问题

但是总有希望尽可能发挥电脑全部性能的时候，这时你可以选择通过新增下面的注册表值来禁用该补丁

```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management]
"FeatureSettingsOverride"=dword:00000003
"FeatureSettingsOverrideMask"=dword:00000003
```

## 通过注册表进行映像劫持

映像劫持，可以让用户在运行一个可执行文件的时候，被注入的另一个程序所代替

下面以安装在  `C:\Program Files\7-Zip\7zFM.exe` 的 7Zip 注入到  `Explorer.exe` 作为例子讲解

首先需要在 `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options]` 下创建一个名为 `explorer.exe` 的键

然后再其内创建一个名为 `Debugger` 的值，类型为 `字符串值 (REG_SZ)`， 值则为 7Zip 的可执行文件完整路径

```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\explorer.exe]
"Debugger"="C:\\Program Files\\7-Zip\\7zFM.exe"
```

设置完成后，重启电脑，即可发现这时系统不再在登入用户账户后，自动启动 `explorer.exe` 所自带的桌面环境，转而启动了 7Zip

## 通过命令行工具管理服务项

1. 列出所有服务

   ```
   sc query type= service state= all
   ```

2. 只列出所有服务名称

   ```
   sc query type= service state= all | find /i "SERVICE_NAME:"
   ```

3. 查找特定的服务

   ```
   sc query type= service state= all | find /i "SERVICE_NAME: 要查找的服务名称"
   ```

4. 显示特定服务的详细情况

   ```
   sc query 服务名称
   ```

5. 查找正在运行的服务

   1. `sc query type= service`
   2. `net start`

6. 查找所有停止的服务

   ```
   sc query type= service state= inactive
   ```

7. 启动一项服务<br>⚠注意: 这里需要用的是 **<i>服务名称 (SERVICE_NAME)</i>** ，而非显示名称 (DISPLAY_NAME)

   ```
   net start 服务名称
   ```

8. 停止一项服务<br>⚠注意: 这里需要用的是 **<i>服务名称 (SERVICE_NAME)</i>** ，而非显示名称 (DISPLAY_NAME)

   ```
   net stop 服务名称
   ```

9. 禁用一项服务<br>⚠注意: 这里需要用的是 **<i>服务名称 (SERVICE_NAME)</i>** ，而非显示名称 (DISPLAY_NAME)

   ```
   sc config 服务名称 start= disabled
   ```

10. 启用一项服务<br>⚠注意: 这里需要用的是 **<i>服务名称 (SERVICE_NAME)</i>** ，而非显示名称 (DISPLAY_NAME)

   ```
   REM delayed-auto = 自动(延迟启动)
   REM auto         = 自动
   REM demand       = 手动

   sc config 服务名称 start= auto
   ```

11. 删除一项服务<br>⚠注意: 这里需要用的是 **<i>服务名称 (SERVICE_NAME)</i>** ，而非显示名称 (DISPLAY_NAME)<br>⚠注意: 本操作不可逆，在删除一项系统自带的服务之前，你可以先通过在注册表的 `HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Services` 路径下，导出与服务名相同的注册表项作为备份

   ```
   REM 需要管理员权限，若管理员权限仍然不够，那么你可能需要 TrustedInstaller 权限
   sc delete 服务名称
   ```

## 通过命令行工具管理计划任务

1. 列出所有计划任务

   ```
   schtasks /query
   ```

   示例输出:

   ```
   文件夹: \Microsoft\Windows\RecoveryEnvironment
   任务名            下次运行时间       模式
   ================ ================ ================
   VerifyWinRE      N/A              已禁用
   ```

2. 删除特定计划任务<br>本例中使用上一条命令的输出作为示例，删除时需要提供 **<i>完整</i>** 的任务计划名（即文件夹 + 任务名）

   ```
   REM /f 参数不是必须的，如果不加这个参数，删除时就会弹出确认选项

   schtasks /delete /tn "\Microsoft\Windows\RecoveryEnvironment\VerifyWinRE" /f
   ```

3. 禁用特定的计划任务

   ```
   schtasks /change /tn "完整的任务计划名" /disable
   ```

4. 启用特定的计划任务

   ```
   schtasks /change /tn "完整的任务计划名" /enable
   ```

## 启用或禁用「基于虚拟化的安全性」

> ⚠ 注意：关闭后将会影响虚拟机的使用

以管理员身份运行下面的命令

```
REM 关闭
bcdedit /set hypervisorlaunchtype off

REM 打开
bcdedit /set hypervisorlaunchtype auto
```

查询方法

运行 `msinfo32` 打开 *系统信息* 工具，在 *系统摘要* 下找到 *基于虚拟化的安全性*

## 通过注册表降低网络延迟

![通过注册表降低网络延迟](https://github-share-1304366332.cos.ap-guangzhou.myqcloud.com/softUsage/operatingSystem/windows/img0001.png)

打开 **注册表编辑器** 然后定位到以下键 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces`，这时你应该能在左边的窗格中看到很多由UUID命名的子键

逐个打开并确认这些子键其中的 `DhcpServer` 值是否跟你的网络环境相互，如果相符，则添加下列两个 `DWORD(32位)值`，两个值的数据均为 `1`

+ `TcpAckFrequency`
+ `TCPNoDelay`

## 删除 *此电脑* 里面的 *3D 对象*

> 其他的 *文件夹* 也是同理，但这里不展开说，因为我习惯会保留住方便快捷访问，对于我个人来说，只有 *3D 对象* 是用不到的

打开 **注册表编辑器** 然后定位到以下键  `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\MyComputer\NameSpace`

然后删除名为 `{0DB7E03F-FC29-4DC6-9020-FF41B59E513A}` 的键

## Microsoft Store 应用安装失败，无法为 App 创建 AppContainer 配置文件

错误截图如下：

![AppContainerError](https://github-share-1304366332.cos.ap-guangzhou.myqcloud.com/softUsage/operatingSystem/windows/img0002.png)

详细错误原因：

`应用安装失败，错误消息: 错误 0x80070005: Windows 无法为 AppleInc.iCloud_14.2.108.0_x64__nzyj5cx40ttqa 程序包创建 AppContainer 配置文件。 (0x80070005)`

用 **<i>管理员身份</i>** 的 *PowerShell* 运行下方的命令即可：

`Get-AppXPackage -AllUsers -Name App包的PackageName | Foreach {Add-AppxPackage -DisableDevelopmentMode -Register "$($_.InstallLocation)\AppXManifest.xml" -Verbose}`

在本例中， **<i>App包的PackageName</i>** 应该为 `AppleInc.iCloud` ， *App包的PackageName* 可以在错误原因里面查到

示例输出：

```text
PS C:\Windows\system32> Get-AppXPackage -AllUsers -Name AppleInc.iCloud | Foreach {Add-AppxPackage -DisableDevelopmentMode -Register "$($_.InstallLocation)\AppXManifest.xml" -Verbose}

详细信息: 正在目标“C:\Program Files\WindowsApps\AppleInc.iCloud_14.2.108.0_x64__nzyj5cx40ttqa\AppXManifest.xml”上执行操作“注册程序包”。
详细信息: 操作完成: C:\Program Files\WindowsApps\AppleInc.iCloud_14.2.108.0_x64__nzyj5cx40ttqa\AppXManifest.xml
```

<sub> \* . [引用来源](https://answers.microsoft.com/zh-hans/windows/forum/all/%E5%BE%AE%E8%BD%AF%E5%BA%94%E7%94%A8%E5%95%86/1ed45936-e599-4524-9616-5263c7031c13) </sub>

---

[上一级](../..)

[笔记首页](/)