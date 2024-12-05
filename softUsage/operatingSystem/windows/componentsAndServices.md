# 组件与服务速查

## Windows 10 服务列表

仅针对系统版本 `19045.5073 22H2`

服务的注册表文件位于 `X:/Windows/System32/config/SYSTEM\ControlSet001\Services`

可以通过 *注册表编辑器* 的 **加载配置单元** 功能来加载离线系统的注册表进行编辑

\*. 有些服务的注册表键跟目录不包含 *启动类型 (Start)* 及 *服务类型 (Type)* 键值，本表将不包含这种类型的服务，如 `.NET CLR Data` 、 `adsi` 等等

### 启动类型

|中文名称|注册表对应的 *Start* 键值|
|----|----|
|引导|0|
|系统|1|
|自动|2|
|手动|3|
|禁用|4|

### 服务类型

|名称|注册表对应的 *Type* 键值<br>16 进制|
|----|----|
|Kernel|1|
|FileSys|2|
|Own|10|
|Share|20|
|User share process template|60|
|||

### 服务列表

|服务名称<sup>1</sup>|显示名称 (EN)<sup>2</sup>|默认启动类型|优化后启动类型<sup>3, 4</sup>|服务类型<sup>5</sup>|备注<sup>6</sup>|
|----|----|----|----|----|----|
|1394ohci|1394 OHCI Compliant Host Controller|3|-|1|1394 OpenHCI Driver by Microsoft Corporation|
|3ware|3ware|0|3|1|LSI 3ware SCSI Storport Driver by LSI|
|ACPI|Microsoft ACPI Driver|0|-|1|ACPI Driver for NT by Microsoft Corporation<br>更改此项服务将会导致系统 **无法启动**|
|AcpiDev|ACPI Devices driver|3|-|1|ACPI Devices Driver by Microsoft Corporation|
|acpiex|Microsoft ACPIEx Driver|0|-|1|ACPIEx Driver by Microsoft Corporation<br>更改此项服务将会导致系统 **无法启动**|
|acpipagr|ACPI Processor Aggregator Driver|3|-|1|ACPI Processor Aggregator Device Driver by Microsoft Corporation|
|AcpiPmi|ACPI Power Meter Driver|3|-|1|ACPI Power Metering Driver by Microsoft Corporation|
|acpitime|ACPI Wake Alarm Driver|3|-|1|ACPI Wake Alarm by Microsoft Corporation|
|Acx01000|Acx01000|3|-|1|Audio KMDF Class Extension by Microsoft Corporation|
|ADP80XX|ADP80XX|0|3|1|PMC-Sierra Storport Driver For SPC8x6G SAS/SATA controller by PMC-Sierra|
|AFD|Ancillary Function Driver for Winsock|1|-|1|Ancillary Function Driver for Winsock<br>未测试，可能影响所有网络 Winsock ，不建议禁用|
|ahcache|Application Compatibility Cache|1|-|1|禁用后 **开始菜单** 无法打开<br>UWP 功能将受影响|
|AppID|AppID Driver|3|-|1|UWP 相关|
|AppIDSvc|Application Identity|3|-|20|UWP 相关|
|Appinfo|Application Information|3|-|20|UWP 相关<br>影响需要管理员权限的应用软件启动|
|applockerfltr|Smartlocker Filter Driver|3|-|1|用于鉴别签名过的安装包？|
|AppMgmt|Application Management|3|-|20|与安装卸载程序，及安装卸载过程中枚举组策略项目有关|
|AppReadiness|App Readiness|3|4|20|新用户账户首次登入时，自动安装并配置 UWP<br>本服务在某些情况下会导致桌面黑屏 Bug ，具体请自行 Google|
|AppXSvc|AppX Deployment Service (AppXSVC)|3|-|20|UWP 相关|
|arcsas|Adaptec SAS/SATA-II RAID Storport's Miniport Driver|0|3|1|Adaptec SAS RAID WS03 Driver by PMC-Sierra, Inc|
|AsyncMac|RAS Asynchronous Media Driver|3|-|1|RAS Asynchronous Media Driver<br>影响与网络相关的 RAS 鉴权|
|atapi|IDE Channel|0|3|1|ATAPI IDE Miniport Driver by Microsoft Corporation<br>若不再使用 IDE 硬盘，可以考虑禁用，虚拟机用户请关注硬盘接口类型|
|AudioEndpointBuilder|Windows Audio Endpoint Builder|2|-|20|管理 Windows 声音设备的服务|
|Audiosrv|Windows Audio|2|-|10|Windows 声音相关|
|AxInstSV|ActiveX Installer (AxInstSV)|3|-|20|UAC 控制相关|
|b06bdrv||0|3|1|Broadcom NetXtreme II VBD Driver|
|bam|Background Activity Moderator Driver|1|-|1|后台进程管理服务|
|BasicDisplay|BasicDisplay|1|-|1|Microsoft Basic Display Driver by Microsoft Corporation<br>待测试|
|BasicRender|BasicRender|1|-|1|Microsoft Basic Render Driver by Microsoft Corporation<br>待测试|
|BcastDVRUserService|GameDVR and Broadcast User Service|3|-|60||
|bcmfn2|Bcmfn2 Service|3|-|1|BCM Function 2 Device Driver by Windows (R) Win 7 DDK provider<br>博通网卡驱动？|
|Beep|Beep|2|3|1|可能是主板的蜂鸣器驱动？|
|BFE|Base Filtering Engine|2|3|20|Windows 防火墙及 IPsec 相关|
|bindflt|Windows Bind Filter Driver|2|-|2|文件系统相关|
|BITS|Background Intelligent Transfer Service|2|4|20|Windows Update 相关<sup>7</sup>|
|BluetoothUserService|Bluetooth User Support Service|3|-|60|蓝牙相关|
|bowser|Bowser|3|-|2|域控AD文件系统相关|
|BrokerInfrastructure|Background Tasks Infrastructure Service|2|-|20|后台进程管理服务|
|BTAGService|Bluetooth Audio Gateway Service|3|-|20|蓝牙音频相关|
|BthA2dp|Microsoft Bluetooth A2dp driver|3|-|1|蓝牙相关|
|BthAvctpSvc|AVCTP service|3|-|20|蓝牙视频、音频控制传输服务|
|||||||
|||||||
|||||||
|||||||
|||||||
|||||||

#### 其他查找不到信息的未知服务

|服务名称<sup>1</sup>|显示名称 (EN)<sup>2</sup>|默认启动类型|优化后启动类型<sup>3, 4</sup>|服务类型<sup>5</sup>|备注<sup>6</sup>|
|----|----|----|----|----|----|
|amdgpio2||3||1||
|amdi2c||3||1||
|AmdK8||3||1||
|AmdPPM||3||1||
|amdsata||0||1||
|amdsbs||0||1||
|amdxata||0||1||

1. 该服务在 *注册表 (Regedit.exe)* 中的 *键名*
2. 该服务在 *服务 (services.msc)* 中的 *显示名称*
3. `-` 代表不建议优化
4. 优化建议仅针对非公司环境的个人电脑
5. 该值为 *注册表 (Regedit.exe)* 中的 **16 进制** 值(打开值编辑时的默认选项)
6. 资料来源为 [batcmd](https://batcmd.com/windows/10/services/) 、 [Revert Service](https://revertservice.com/10/) 以及个人实机测试
7. 禁用 Windows Update 相关后，无法从 Microsoft Store 安装和更新应用，但你可以通过 [Microsoft Store - Generation Project (v1.2.3) \[by @rgadguard & mkuba50\]](https://store.rg-adguard.net) ，来下载想要安装应用的 Appx 软件包进行本地安装

[上一级](../README.md)

[笔记首页](../../../README.md)
