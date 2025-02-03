# 组件与服务速查

## Windows 10 服务列表

仅针对系统版本 `19045.5073 22H2`

服务的注册表文件位于 `X:/Windows/System32/config/SYSTEM\ControlSet001\Services`

可以通过 *注册表编辑器* 的 **加载配置单元** 功能来加载离线系统的注册表进行编辑

\*. 有些服务的注册表键根目录不包含 *启动类型 (Start)* 及 *服务类型 (Type)* 键值，本表将不包含这种类型的服务，如 `.NET CLR Data` 、 `adsi` 等等

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
|User own process template|50|
|User share process template|60|
|||

### 服务列表

|服务名称<sup>1</sup>|显示名称<sup>2</sup>|默认启动类型|优化后启动类型<sup>3, 4</sup>|服务类型<sup>5</sup>|备注<sup>6, 7</sup>|
|----|----|----|----|----|----|
|1394ohci|1394 OHCI Compliant Host Controller|3|-|1|微软开发的 1394 驱动|
|3ware||0|3|1|LSI 3ware SCSI 驱动|
|AarSvc|Agent Activation Runtime|3||60|<u>Runtime for activating conversational agent applications</u>|
|ACPI|Microsoft ACPI Driver|0|-|1|ACPI Driver for NT by Microsoft Corporation<br>更改此项服务将会导致系统 **无法启动**|
|AcpiDev|ACPI Devices driver<br>ACPI 设备驱动程序|3|-|1|微软开发的 ACPI 驱动|
|acpiex|Microsoft ACPIEx Driver|0|-|1|ACPIEx Driver by Microsoft Corporation<br>更改此项服务将会导致系统 **无法启动**|
|acpipagr|ACPI Processor Aggregator Driver<br>ACPI 处理器聚合器驱动程序|3|-|1|微软开发的 ACPI 驱动|
|AcpiPmi|ACPI Power Meter Driver<br>ACPI 电源表驱动程序|3|-|1|微软开发的 ACPI 驱动|
|acpitime|ACPI Wake Alarm Driver<br>ACPI 唤醒警报驱动程序|3|-|1|微软开发的 ACPI 驱动|
|Acx01000||3|-|1|Audio KMDF Class Extension by Microsoft Corporation|
|ADP80XX||0|3|1|PMC-Sierra Storport Driver For SPC8x6G SAS/SATA controller by PMC-Sierra|
|AFD|Ancillary Function Driver for Winsock|1|-|1|<u>Ancillary Function Driver for Winsoc</u><br>未测试，可能影响所有网络 Winsock ，不建议禁用|
|afunix|afunix|1||1|???|
|ahcache|Application Compatibility Cache|1|-|1|<u>Cache Compatibility Data and Attributes for Individual PE File</u>禁用后 **开始菜单** 无法打开<br>UWP 功能将受影响|
|AJRouter|AllJoyn Router Service|3|-|20|<u>路由本地 AllJoyn 客户端的 AllJoyn 消息。如果停止此服务，则自身没有捆绑路由器的 AllJoyn 客户端将无法运行。</u><br>会被 NTLite 精简，可禁用|
|ALG|Application Layer Gateway Service|3|-|10|<u>为 Internet 连接共享提供第三方协议插件的支持</u><br>会被 NTLite 精简，可禁用|
|AppID|AppID Driver<br>AppID 驱动程序|3|-|1|<u>标识应用程序并强制执行软件限制策略。</u><br>UWP 相关|
|AppIDSvc|Application Identity|3|-|20|<u>确定并验证应用程序的标识。禁用此服务将阻止强制执行 AppLocker。</u><br>UWP 相关|
|Appinfo|Application Information|3|-|20|<u>使用辅助管理权限便于交互式应用程序的运行。如果停止此服务，用户将无法使用辅助管理权限启动应用程序，而执行所需用户任务可能需要这些权限。</u><br>UWP 相关<br>影响需要管理员权限的应用软件启动|
|applockerfltr|Smartlocker Filter Driver<br>Smartlocker 筛选器驱动程序|3|-|1|<u>标识由授权的安装程序创建的文件。</u><br>用于鉴别签名过的安装包？|
|AppMgmt|Application Management|3|-|20|<u>为通过组策略部署的软件处理安装、删除以及枚举请求。如果该服务被禁用，则用户将不能安装、删除或枚举通过组策略部署的软件。如果此服务被禁用，则直接依赖于它的所有服务都将无法启动。</u><br>与安装卸载程序，及安装卸载过程中枚举组策略项目有关|
|AppReadiness|App Readiness|3|4|20|<u>当用户初次登录到这台电脑和添加新应用(UWP?)时，使应用进入就绪可用的状态。</u><br>本服务在某些情况下会导致桌面黑屏 Bug ，具体请自行 Google|
|AppVClient|Microsoft App-V Client|4|-|10|<u>Manages App-V users and virtual applications</u><br>会被 NTLite 精简，可禁用|
|AppvStrm|AppvStrm|3|4|2|<u>Microsoft App-V Streaming Mini-Filter Driver</u><br>会被 NTLite 精简，可禁用|
|AppvVemgr|AppvVemgr|3|4|2|<u>Microsoft App-V Virtual Environment Manager Driver</u><br>会被 NTLite 精简，可禁用|
|AppvVfs|AppvVfs|3|4|2|<u>Microsoft App-V VFS Mini-Filter Driver</u><br>会被 NTLite 精简，可禁用|
|AppXSvc|AppX Deployment Service (AppXSVC)|3|-|20|<u>为部署 Microsoft Store 应用程序提供基础结构支持。此服务根据需要启动，如果已禁用的 Microsoft Store 应用程序未部署到系统，此服务可能无法正常工作。</u><br>UWP 相关|
|arcsas|Adaptec SAS/SATA-II RAID Storport's Miniport Driver|0|3|1|PMC-Sierra 开发的 Adaptec SAS RAID WS03 驱动|
|AssignedAccessManagerSvc|AssignedAccessManager Service<br>AssignedAccessManager 服务|3|4|20|<u>AssignedAccessManager 服务支持 Windows 中的展台体验。</u><br>会被 NTLite 精简，可禁用|
|AsyncMac|RAS Asynchronous Media Driver<br>RAS 异步媒体驱动程序|3|-|1|<u>RAS 异步媒体驱动程序</u><br>影响与网络相关的 RAS 鉴权|
|atapi|IDE Channel<br>IDE 通道|0|3|1|Microsoft 开发的 ATAPI IDE Miniport 驱动<br>若不再使用 IDE 硬盘，可以考虑禁用，虚拟机用户请关注硬盘接口类型|
|AudioEndpointBuilder|Windows Audio Endpoint Builder|2|-|20|<u>管理 Windows 音频服务的音频设备。如果停止了此服务，音频设备和效果将无法正常工作。如果禁用了此服务，任何明确依赖它的服务将无法启动</u>|
|Audiosrv|Windows Audio|2|-|10|<u>管理基于 Windows 的程序的音频。如果此服务被停止，音频设备和效果将不能正常工作。如果此服务被禁用，任何依赖它的服务将无法启动</u>|
|autotimesvc|Cellular Time<br>手机网络时间|3|4|10|<u>此服务基于移动网络中的 NITZ 消息设置时间</u>|
|AxInstSV|ActiveX Installer (AxInstSV)|3|-|20|<u>为从 Internet 安装 ActiveX 控件提供用户帐户控制验证，并基于组策略设置启用对 ActiveX 控件安装的管理。此服务根据要求启动，是否禁用 ActiveX 控件的安装取决于默认浏览器设置。</u><br>UAC 控制相关?|
|b06bdrv|QLogic Network Adapter VBD<br>QLogic 网络适配器 VBD|0|3|1|QLogic 光纤通道适配器、融合网络适配器和智能以太网适配器驱动|
|bam|Background Activity Moderator Driver|1|-|1|<u>Controls activity of background applications</u>|
|BasicDisplay||1|-|1|禁用似乎不影响使用，待测试|
|BasicRender||1|-|1|禁用似乎不影响使用，待测试|
|BcastDVRUserService|GameDVR and Broadcast User Service<br>GameDVR 和广播用户服务|3|4|60|<u>此用户服务用于游戏录制和实况广播</u>|
|BDESVC|BitLocker Drive Encryption Service|3|4|20|<u>BDESVC 承载 BitLocker 驱动器加密服务。BitLocker 驱动器加密为操作系统提供安全启动保障，并为 OS、固定卷和可移动卷提供全卷加密功能。使用此服务，BitLocker 可以提示用户执行与已安装卷相关的各种操作，并自动解锁卷而无需用户交互。此外，它还会将恢复信息存储至 Active Directory (如果这种方法可用并且需要这样做)，并确保使用最新的恢复证书。停止或禁用该服务可以防止用户使用此功能。</u>|
|bcmfn2|bcmfn2 Service|3|-|1|BCM Function 2 Device Driver by Windows (R) Win 7 DDK provider??|
|Beep|Beep|2|3|1|可能是主板的蜂鸣器驱动？|
|BFE|Base Filtering Engine|2|4|20|<u>基本筛选引擎(BFE)是一种管理防火墙和 Internet 协议安全(IPsec)策略以及实施用户模式筛选的服务。停止或禁用 BFE 服务将大大降低系统的安全。还将造成 IPsec 管理和防火墙应用程序产生不可预知的行为。</u>|
|bindflt|Windows Bind Filter Driver|2|-|2|<u>Binds filesystem namespaces to different locations and hides this remapping from the user</u><br>将文件系统命名空间绑定到不同位置，并向用户隐藏这种重新映射??|
|BITS|Background Intelligent Transfer Service|2|4|20|<u>使用空闲网络带宽在后台传送文件。如果该服务被禁用，则依赖于 BITS 的任何应用程序(如 Windows 更新或 MSN Explorer)将无法自动下载程序和其他信息。</u><sup>8</sup>|
|BluetoothUserService|Bluetooth User Support Service<br>蓝牙用户支持服务|3|-|60|<u>蓝牙用户服务支持与每个用户会话相关的蓝牙功能的正确运行。</u>|
|bowser|Bowser<br>浏览器|3|4|2|<u>NT Lan 管理器数据报接收器驱动程序</u><br>即将被 Microsoft 弃用的旧技术|
|BrokerInfrastructure|Background Tasks Infrastructure Service|2|-|20|<u>控制哪些后台任务可以在系统上运行的 Windows 基础结构服务。</u>|
|BTAGService|Bluetooth Audio Gateway Service<br>蓝牙音频网关服务|3|-|20|<u>支持蓝牙免提配置文件的音频网关角色的服务。</u>|
|BthA2dp|Microsoft Bluetooth A2dp driver|3|-|1|蓝牙相关驱动|
|BthAvctpSvc|AVCTP service<br>AVCTP 服务|3|-|20|<u>这是音频视频控制传输协议服务</u>|
|BthEnum|Bluetooth Enumerator Service<br>蓝牙枚举器服务|3|-|1||
|BthHFEnum|Microsoft Bluetooth Hands-Free Profile driver<br>Microsoft Bluetooth 免提配置文件驱动程序|3|-|1||
|BthLEEnum|Bluetooth Low Energy Driver<br>蓝牙低能耗驱动程序|3|-|1||
|BthMini|Bluetooth Radio Driver<br>蓝牙无线收发器驱动程序|3|-|1||
|BTHMODEM|Bluetooth Modem Communications Driver<br>蓝牙调制解调器通信驱动程序|3|-|1||
|BTHPORT|Bluetooth Port Driver<br>蓝牙端口驱动程序|3|-|1||
|bthserv|Bluetooth Support Service<br>蓝牙支持服务|3|-|20|<u>蓝牙服务支持发现和关联远程蓝牙设备。停止或禁用此服务可能会导致已安装的蓝牙设备无法正常运行，并使新设备无法被发现或关联。</u>|
|BTHUSB|Bluetooth Radio USB Driver<br>蓝牙无线电收发器 USB 驱动程序|3|-|1||
|bttflt|Microsoft Hyper-V VHDPMEM BTT Filter<br>Microsoft Hyper-V VHDPMEM BTT 筛选器|0|-|1||
|buttonconverter|Service for Portable Device Control devices<br>针对便携式设备控制装置的服务|3|-|1|部分 HID 设备的驱动，如触屏等|
|CAD|Charge Arbitration Driver<br>充电均衡驱动程序|3|-|1|笔记本充电相关，台式机可禁用<br>待测试|
|camsvc|Capability Access Manager Service<br>功能访问管理器服务|3|-|20|<u>提供设施，用于管理 UWP 应用对应用功能的访问权限以及检查应用的特定应用功能访问权限</u>|
|CaptureService|CaptureService|3|-|60|<u>为调用 Windows.Graphics.Capture API 的应用程序启用可选的屏幕捕获功能。</u>|
|cbdhsvc|Clipboard User Service<br>剪贴板用户服务|3|4|60|<u>此用户服务用于剪贴板方案</u><br>会被 NTLite 精简，可禁用，可用开源的 [CopyQ](https://github.com/hluk/CopyQ) 代替|
|cdfs|CD/DVD File System Reader|4|-|2|<u>ISO9660/Joliet File System Reader for CD/DVDs. (Core) (All pieces)</u><br>CD/DVD 文件系统<br>待测试，是否影响 ISO 文件挂载|
|CDPSvc|Connected Devices Platform Service<br>连接设备平台服务|2|3|20|<u>此服务用于连接设备平台方案</u><br>可能与打印机、扫描仪相关，但不确定<br>也有说法是仅在与 Xbox 连接时有用<br>待测试，可以先禁用看看|
|CDPUserSvc|Connected Devices Platform User Service<br>连接设备平台用户服务|2|3|60|<u>此用户服务用于连接设备平台方案</u><br>可能与打印机、扫描仪相关，但不确定<br>也有说法是仅在与 Xbox 连接时有用<br>待测试，可以先禁用看看|
|cdrom|CD-ROM Driver|1||1|待测试，是否影响 ISO 文件挂载|
|CertPropSvc|Certificate Propagation|3|-|20|<u>将用户证书和根证书从智能卡复制到当前用户的证书存储，检测智能卡何时插入到智能卡读卡器中，并在需要时安装智能卡即插即用微型驱动器。</u>|
|cht4iscsi||0|4|1|作用不明，禁用之<br>根据 [batcmd](https://batcmd.com/windows/11/services/cht4iscsi/) 的描述，此服务仅存在于 Windows 11|
|cht4vbd|Chelsio Virtual Bus Driver<br>Chelsio 虚拟总线驱动程序|3|4|1|Chelsio 光线网卡驱动<br>根据 [batcmd](https://batcmd.com/windows/11/services/cht4vbd/) 的描述，此服务仅存在于 Windows 11|
|CimFS||1|4|2|类似 WIM 文件的另一种备份格式: Cim 文件的挂载支持<br>没听说过的东西，先禁用之|
|circlass|Consumer IR Devices|3|4|1|红外线支持|
|CldFlt|Windows Cloud Files Filter Driver|2|-|2|云文件筛选器驱动<br>待测试，不知是否影响 iCloud (个人需求)|
|CLFS|Common Log (CLFS)|0|-|1|<u>General-purpose logging service</u><br>更改此项服务将会导致系统 **无法启动**|
|ClipSVC|Client License Service (ClipSVC)|3|-|20|<u>提供对 Microsoft Store 的基础结构支持。此服务按需启动，并且如果禁用了此服务，则使用 Windows Store 购买的应用程序将无法正常运行。</u>|
|CmBatt|Microsoft ACPI Control Method Battery Driver<br>Microsoft ACPI 控制方法电池驱动程序|3|-|1||
|CNG||0|-|1|<u>CNG 的关键价值主张之一是加密灵活性，有时称为与加密不可知性。 但是，需要将安全套接字层协议 (SSL) 或传输层安全性 (TLS)、CMS (S/MIME)、IPsec、Kerberos 等协议的实现转换为 CNG，以使此功能具有价值。 在 CNG 级别，必须为所有算法类型（对称、非对称、哈希函数）、随机数生成和其他实用工具函数提供替换和可发现性。 协议级别更改更为重要，因为在许多情况下，协议 API 需要添加以前不存在的算法选择和其他灵活性选项。<br>CNG 首先在 Windows Vista 中可用，并定位为在整个 Microsoft 软件堆栈中取代 CryptoAPI 的现有用途。</u><sup>9</sup><br>更改此项服务将会导致系统 **无法启动**|
|cnghwassist|CNG Hardware Assist algorithm provider|4|-|1|参见 **CNG**|
|CompositeBus|Composite Bus Enumerator Driver<br>复合总线枚举器驱动程序|3|-|1|可能于 MTP 设备驱动有关<sup>10</sup>|
|COMSysApp|COM+ System Application|3|-|10|<u>停止该服务，则大多数基于 COM+ 的组件将不能正常工作。如果禁用该服务，则任何明确依赖它的服务都将无法启动。</u>|
|condrv|Console Driver|3|-|1|处理各种终端模拟器 ( CMD 、 PowerShell 等 ) 与终端 ( conhost.exe ) 之间的通讯|
|ConsentUxUserSvc|ConsentUX User Service<br>ConsentUX|3|4|60|<u>允许 ConnectUX 和电脑设置连接 WLAN 显示器和蓝牙设备并与其配对。</u><br>ConnectUX 已被弃用|
|CoreMessagingRegistrar|CoreMessaging|2|-|20|<u>Manages communication between system components.</u>|
|CredentialEnrollmentManagerUserSvc|CredentialEnrollmentManagerUserSvc|3|-|50|<u>凭据注册管理器</u>|
|CryptSvc|Cryptographic Services|2|-|20|<u>提供三种管理服务: 编录数据库服务，用于确认 Windows 文件的签名和允许安装新程序；受保护的根服务，它从此计算机添加和删除受信任的根证书颁发机构的证书；自动根证书更新服务，用于从 Windows 更新中检索根证书和启用 SSL 等方案。如果此服务已停止，这些管理服务将无法正常运行。如果此服务已禁用，任何明确依赖它的服务将无法启动。</u>|
|CSC|Offline Files Driver|1|4|1|<u>允许在本地计算机处于脱机状态时使用网络文件。</u><br>Home 版不存在，可禁用之|
|CscService|Offline Files|4|-|20|<u>脱机文件服务在脱机文件缓存中执行维护活动，响应用户登录和注销事件，实现公共 API 的内部部分，并将相关的事件分配给关心脱机文件活动和缓存更改的用户。</u><br>Home 版不存在，可禁用之|
|dam|Desktop Activity Moderator Driver|1|-|1|<u>Controls activity of desktop applications</u><sup>11</sup><br>当系统即将进入 S3 睡眠状态时，暂停或限制桌面软件的运行状态以节省电力|
|DcomLaunch|DCOM Server Process Launcher|2|-|20|<u>DCOMLAUNCH 服务可启动 COM 和 DCOM 服务器，以响应对象激活请求。如果此服务被停用或禁用，则使用 COM 或 DCOM 的程序将无法正常工作。强烈建议你运行 DCOMLAUNCH 服务。</u>|
|defragsvc|Optimize drives|3|4|10|<u>通过优化存储驱动器上的文件来帮助计算机更高效地运行。</u><br>经典巨硬式不说人话翻译，人话：定期运行 **磁盘碎片整理** 对于 SSD 有害无利，禁用之|
|DeviceAssociationBrokerSvc|DeviceAssociationBroker|3|-|60|<u>Enables apps to pair devices</u><br>待测试，1903 之前不存在，估计是允许 UWP 与某些硬件配对|
|DeviceAssociationService|Device Association Service|3|-|20|<u>在系统与有线或无线设备之间启用匹配。</u>|
|DeviceInstall|Device Install Service|3|-|20|<u>使计算机在极少或没有用户输入的情况下能识别并适应硬件的更改。终止或禁用此服务会造成系统不稳定。</u>|
|DevicePickerUserSvc|DevicePicker|3|4|3|<u>此用户服务用于管理 Miracast、DLNA 和拨号用户界面</u><br>会被 NTLite 精简，可禁用|
|DevicesFlowUserSvc|DevicesFlow|3|-|60|<u>允许 ConnectUX 和电脑设置连接 WLAN 显示器和蓝牙设备并与其配对。</u><br>待测试，ConnectUX 已被弃用|
|DevQueryBroker|DevQuery Background Discovery Broker|3|-|10|<u>使应用能够发现具有后台任务的设备</u><br>经典巨硬式不说人话翻译，人话：后台定期扫描，以发现新设备，并通知系统自动注册新设备|
|Dfsc|DFS Namespace Client Driver|1|-|2|<u>用于访问 DFS 命名空间的客户端驱动程序</u><br>Windows 共享网络别名支持，如 `\\Contoso\Public` 等|
|Dhcp|DHCP Client|2|-|20|<u>将不能接收动态 IP 地址和 DNS 更新。如果此服务被禁用，所有明确依赖它的服务都将不能启动。</u><br>你上网吗？|
|diagnosticshub.standardcollector.service|Microsoft (R) 诊断中心标准收集器服务|3|4|10|<u>诊断中心标准收集器服务。运行时，此服务会收集实时 ETW 事件，并对其进行处理。</u><br>诊断不了故障的故障诊断功能支持|
|diagsvc|Diagnostic Execution Service|3|4|20|<u>Executes diagnostic actions for troubleshooting support</u><br>诊断不了故障的故障诊断功能支持|
|DiagTrack|Connected User Experiences and Telemetry|2|4|10|<u>Connected User Experiences and Telemetry</u><br>用户体验数据收集|
|disk|Disk Driver<br>磁盘驱动程序|0|-|1||
|DispBrokerDesktopSvc|Display Policy Service<br>显示策略服务|2|3|20|待测试，远程显示器支持|
|DisplayEnhancementService|Display Enhancement Service<br>显示增强服务|3|-|20|<u>用于管理显示增强(如亮度控制)的服务。</u>|
|DmEnrollmentSvc|Device Management Enrollment Service<br>设备管理注册服务|3|-|10|<u>为设备管理执行设备注册活动</u><br>企业远程系统配置及硬件管理|
|dmwappushservice|Device Management Wireless Application Protocol (WAP) Push message Routing Service<br>设备管理无线应用程序协议 (WAP) 推送消息路由服务|3|-|20|<u>路由设备收到的无线应用程序协议 (WAP) 推送消息并同步设备管理会话</u>|
|Dnscache|DNS Client|2|-|20|<u>DNS 客户端服务(dnscache)缓存域名系统(DNS)名称并注册该计算机的完整计算机名。如果该服务被停止，将继续解析 DNS 名称。然而，将不缓存 DNS 名称的查询结果，且不注册计算机名。如果该服务被禁用，则任何明确依赖于它的服务都将无法启动。</u>|
|DoSvc|Delivery Optimization|3|4|20|<u>执行内容传递优化任务</u><sup>8</sup>|
|dot3svc|Wired AutoConfig|3|-|20|<u>有线自动配置(DOT3SVC)服务负责对以太网接口执行 IEEE 802.1X 身份验证。如果当前有线网络部署强制执行 802.1X 身份验证，则应配置 DOT3SVC 服务运行以用于建立第 2 层连接性和/或用于提供对网络资源的访问权限。DOT3SVC 服务会影响到强制执行 802.1X 身份验证的有线网络。</u>|
|DPS|Diagnostic Policy Service|2|4|20|<u>诊断策略服务启用了 Windows 组件的问题检测、疑难解答和解决方案。如果该服务被停止，诊断将不再运行。</u>|
|drmkaud|Microsoft Trusted Audio Drivers|3|-|1|音频驱动|
|DsmSvc|Device Setup Manager|3|4|20|<u>支持检测、下载和安装与设备相关的软件。如果此服务被禁用，则可能使用过期软件对设备进行配置，因此设备可能无法正常工作。</u><br>用于通过 Windows Update 来自动更新驱动，会造成 CPU 占用异常高的情况，建议禁用|
|DsSvc|Data Sharing Service|3|4|20|<u>提供应用程序之间的数据代理。</u><br>待测试，连巨硬员工都不知道这是什么东西的神秘服务<br>根据搜索，与 Samba 共享有关，若提供(还是访问也需要?) Samba 服务，此服务必须开启<sup>12</sup>|
|DusmSvc|Data Usage<br>数据使用量|2|4|10|<u>网络数据使用量，流量上限，限制背景数据，按流量计费的网络。</u>|
|DXGKrnl|LDDM Graphics Subsystem|1|-|1|<u>Controls the underlying video driver stacks to provide fully-featured display capabilities.</u><br>DirectX 图形内核子系统|
|Eaphost|Extensible Authentication Protocol|3|-|20|<u>可扩展的身份验证协议(EAP)服务在以下情况下提供网络身份验证: 802.1x 有线和无线、VPN 和网络访问保护(NAP)。EAP 在身份验证过程中也提供网络访问客户端使用的应用程序编程接口(API)，包括无线客户端和 VPN 客户端。如果禁用此服务，该计算机将无法访问需要 EAP 身份验证的网络。</u>|
|ebdrv|QLogic 10 Gigabit Ethernet Adapter VBD|0|4|1|QLogic 10G 网卡驱动|
|EFS|Encrypting File System (EFS)|3|4|20|<u>提供用于在 NTFS 文件系统卷上存储加密文件的核心文件加密技术。如果停止或禁用此服务，则应用程序将无法访问加密的文件。</u><br>待测试，目测与 BitLocker 相关|
|EhStorClass|Enhanced Storage Filter Driver|0|-|1|<u>Enhanced Storage Filter Driver</u><br>待测试，目测与加密相关|
|EhStorTcgDrv|Microsoft driver for storage devices supporting IEEE 1667 and TCG protocols<br>支持 IEEE 1667 和 TCG 协议的 Microsoft 存储设备驱动程序|1|-|1|待测试，目测与加密相关|
|embeddedmode|Embedded Mode<br>嵌入模式|3|4|20|<u>嵌入模式服务启用与后台应用程序相关的方案。禁用此服务会阻止激活后台应用程序。</u><br>IoT 版本的特殊功能|
|EntAppSvc|Enterprise App Management Service|3|4|20|<u>启用企业应用程序管理。</u>|
|ErrDev|Microsoft Hardware Error Device Driver|3|-|1|目测与设备管理器中，硬件的驱动错误代码相关|
|EventLog|Windows Event Log|2|-|20|<u>此服务管理事件和事件日志。它支持日志记录事件、查询事件、订阅事件、归档事件日志以及管理事件元数据。它可以用 XML 和纯文本两种格式显示事件。停止该服务可能危及系统的安全性和可靠性。</u><br>待测试|
|EventSystem|COM+ Event System|2|-|20|<u>支持系统事件通知服务 (SENS)，此服务为订阅的组件对象模型 (COM) 组件提供自动分布事件功能。如果停止此服务，SENS 将关闭，而且不能提供登录和注销通知。如果禁用此服务，显式依赖此服务的其他服务都将无法启动。</u>|
|exfat|exFAT File System Driver|3|-|2||
|fastfat|FAT12/16/32 File System Driver|3|-|2|<u>Note - dependance on CDROM.SYS only if required to read/write DVD-RAM media (which appears as CD class device). (Core) (All pieces)</u>|
|Fax|Fax|3|4|10|<u>Enables you to send and receive faxes, utilizing fax resources available on this computer or on the network.</u><br>待测试，不知是否会影响扫描仪工作|
|fdc|Floppy Disk Controller Driver<br>软盘控制器驱动程序|3|4|1|今昔是何年|
|fdPHost|Function Discovery Provider Host|3|4|20|<u>FDPHOST 服务承载功能发现(FD)网络发现提供程序。这些 FD 提供程序为简单服务发现协议(SSDP)和 Web 服务发现(WS-D)协议提供网络发现服务。使用 FD 时停止或禁用 FDPHOST 服务将禁用这些协议的网络发现。当该服务不可用时，使用 FD 和依靠这些发现协议的网络服务将无法找到网络服务或资源。</u><br>网络发现功能|
|FDResPub|Function Discovery Resource Publication|3|4|20|<u>发布该计算机以及连接到该计算机的资源，以便能够在网络上发现这些资源。如果该服务被停止，将不再发布网络资源，网络上的其他计算机将无法发现这些资源。</u><br>若在本 PC 共享，本服务可以让该共享资源被其他 PC 发现|
|fhsvc|File History Service|3|4|20|<u>将用户文件复制到备份位置以防意外丢失</u>|
|FileCrypt|FileCrypt|1|4|2|<u>Windows sandboxing and encryption filter.</u><br>待测试|
|FileInfo|File Information FS MiniFilter|0|-|2|<u>Collects information about files in memory to be consumed by other system services.</u>|
|Filetrace|FileTrace|3|-|2|<u>ETW File Trace Filter</u><br>待测试，目测与系统调试有关， ETW = Event Trace for Windows|
|flpydisk|Floppy Disk DriverU<br>软盘驱动程序|3|4|1|今昔是何年|
|FltMgr|FltMgr|0|-|2|<u>文件系统筛选器管理器驱动程序</u><br>更改此项服务将会导致系统 **无法启动**|
|FontCache|Windows Font Cache Service|2||20|<u>通过缓存常用字体数据优化应用程序的性能。如果尚未运行该服务，则应用程序将启动该服务。也可以禁用该服务，但是这样做会降低应用程序性能。</u><br>待测试，真的会降低性能吗？用 Photoshop 2018 测测看|
|FrameServer|Windows Camera Frame Server|3|-|20|<u>允许多个客户端从相机设备访问视频帧。</u><br>摄像头相关|
|FsDepends|File System Dependency Minifilter|3|-|2|<u>This minifilter tracks the dependencies associated with the various nested volumes/filesystems</u><br>更改此项服务将会导致系统 **无法启动**|
|fvevol|BitLocker Drive Encryption Filter Driver|0|-|1|更改此项服务将会导致系统 **无法启动**|
|gencounter|Microsoft Hyper-V Generation Counter|3|-|1|<u>Microsoft Hyper-V 生成计数器</u>|
|genericusbfn|Generic USB Function Class<br>通用 USB 函数类|3|-|1||
|GPIOClx0101|Microsoft GPIO Class Extension Driver|3|-|1||
|gpsvc|Group Policy Client|2|-|20|<u>此服务负责应用管理员通过组策略组件为计算机和用户配置的设置。如果禁用此服务，将不会应用这些设置，并且将无法通过组策略管理应用程序和组件。如果禁用此服务，依赖于组策略组件的所有组件或应用程序都将无法正常运行。</u>|
|GpuEnergyDrv|GPU Energy Driver|1|-|1|<u>Computes energy consumed by GPU</u>|
|GraphicsPerfSvc|GraphicsPerfSvc|3|4|20|<u>Graphics performance monitor service</u><br>Windows 10 Home, Pro, Education, Enterprise (1507, 1511, 1607, 1703) 以上各版本都不包含，禁用之|
|HdAudAddService|Microsoft 1.1 UAA Function Driver for High Definition Audio Service<br>用于 High Definition Audio 服务的 Microsoft 1.1 UAA 函数驱动程序|3|-|1|音频驱动|
|HDAudBus|Microsoft UAA Bus Driver for High Definition Audio<br>用于 High Definition Audio 的 Microsoft UAA 总线驱动程序|3|-|1|音频驱动|
|HidBatt|HID UPS Battery Driver<br>HID UPS 电池驱动程序|3|-|1||
|HidBth|Microsoft Bluetooth HID Miniport|3|-|1|蓝牙相关|
|hidi2c|Microsoft I2C HID Miniport Driver<br>Microsoft I2C HID 微型端口驱动程序|3|-|1||
|hidinterrupt|Common Driver for HID Buttons implemented with interrupts<br>通过中断实施的 HID 按钮的通用驱动程序|3|-|1||
|HidIr|Microsoft Infrared HID Driver|3|4|1|红外线驱动|
|hidserv|Human Interface Device Service|3|-|16|<u>激活键盘、遥控器和其他多媒体设备上的热按钮并继续使用这些按钮。建议你让此服务一直运行。</u>|
|hidspi|Microsoft SPI HID Miniport Driver<br>Microsoft SPI HID 微型端口驱动程序|3|-|1||
|HidUsb|Microsoft HID Class Driver|3|-|1||
|HpSAMD||0||1|HP SAS / SATA 控制器驱动<br>待测试，RAID 卡驱动吗？|
|HTTP|HTTP Service|3||1||
|hvcrash||4|-|1|目测是 Hyper-V 相关服务|
|HvHost|HV 主机服务|3|-|20|<u>为 Hyper-V 虚拟机监控程序提供接口，以便为主机操作系统提供单分区性能计数器。</u>|
|hvservice|Hypervisor/Virtual Machine Support Driver|3|-|1||
|HwNClx0101|Microsoft Hardware Notifications Class Extension Driver|3|4|1|Windows 10 Home, Pro, Education, Enterprise (1507, 1511, 1607, 1703) 以上各版本都不包含，禁用之|
|hwpolicy|Hardware Policy Driver|0|-|1|<u>Contains Processor and other policies</u>|
|hyperkbd||3|-|1|Microsoft VMBus Synthetic Keyboard Driver|
|HyperVideo||3|-|1|Microsoft VMBus Video Device Miniport Driver|
|i8042prt|i8042 Keyboard and PS/2 Mouse Port Driver<br>i8042 键盘和 PS/2 鼠标端口驱动程序|3|-|1||
|iagpio|Intel Serial IO GPIO Controller Driver<br>Intel 串行 IO GPIO 控制器驱动程序|3|-|1||
|iai2c|Intel(R) Serial IO I2C Host Controller<br>Intel(R) 串行 IO I2C 主机控制器|3|-|1||
|iaLPSS2i_GPIO2|Intel(R) Serial IO GPIO Driver v2<br>Intel(R) 串行 IO GPIO 驱动程序 v2|3|-|1||
|iaLPSS2i_GPIO2_BXT_P|Intel(R) Serial IO GPIO Driver v2<br>Intel(R) 串行 IO GPIO 驱动程序 v2|3|-|1||
|iaLPSS2i_GPIO2_CNL|Intel(R) Serial IO GPIO Driver v2<br>Intel(R) 串行 IO GPIO 驱动程序 v2|3|-|1||
|iaLPSS2i_GPIO2_GLK|Intel(R) Serial IO GPIO Driver v2<br>Intel(R) 串行 IO GPIO 驱动程序 v2|3|-|1||
|iaLPSS2i_I2C|Intel(R) Serial IO I2C Driver v2<br>Intel(R) 串行 IO I2C 驱动程序 v2|3|-|1||
|iaLPSS2i_I2C_BXT_P|Intel(R) Serial IO I2C Driver v2<br>Intel(R) 串行 IO I2C 驱动程序 v2|3|-|1||
|iaLPSS2i_I2C_CNL|Intel(R) Serial IO I2C Driver v2<br>Intel(R) 串行 IO I2C 驱动程序 v2|3|-|1||
|iaLPSS2i_I2C_GLK|Intel(R) Serial IO I2C Driver v2<br>Intel(R) 串行 IO I2C 驱动程序 v2|3|-|1||
|iaLPSSi_GPIO|Intel(R) 串行 IO GPIO 主机控制器驱动程序<br>Intel(R) Serial IO GPIO Controller Driver|3|-|1||
|iaLPSSi_I2C|Intel(R) Serial IO I2C Controller Driver<br>Intel(R) 串行 IO I2C 控制器驱动程序|3|-|1||
|iaStorAVC|Intel Chipset SATA RAID Controller<br>Intel 芯片集 SATA RAID 控制器|0|-|1||
|iaStorV|Intel RAID Controller Windows 7|0|-|1||
|ibbus|Mellanox InfiniBand Bus/AL (Filter Driver)<br>Mellanox InfiniBand 总线/AL (筛选器驱动程序)|3|-|1||
|icssvc|Windows Mobile Hotspot Service<br>Windows 移动热点服务|3|-|20|<u>提供与其他设备共享手机网络数据连接的功能。</u>|
|IKEEXT|IKE and AuthIP IPsec Keying Modules|3|-|32|<u>IKEEXT 服务托管 Internet 密钥交换(IKE)和身份验证 Internet 协议(AuthIP)键控模块。这些键控模块用于 Internet 协议安全(IPSec)中的身份验证和密钥交换。停止或禁用 IKEEXT 服务将禁用与对等计算机的 IKE/AuthIP 密钥交换。通常将 IPSec 配置为使用 IKE 或 AuthIP，因此停止或禁用 IKEEXT 服务将导致 IPSec 故障并且危及系统的安全。强烈建议运行 IKEEXT 服务。</u>|
|IndirectKmd|Indirect Displays Kernel-Mode Driver<br>Indirect Displays 内核模式驱动程序|3|-|1|<u>实现了 Indirect Displays 框架的内核模式驱动程序。</u><br>虚拟显示器支持|
|InstallService|Microsoft Store Install Service<br>Microsoft Store 安装服务|3||10|<u>为 Microsoft Store 提供基础结构支持。此服务按需启动，如被禁用，则安装将无法正常运行。</u><br>待测试，不知是否影响本地 Appx 文件的安装|
|intelide||0|-|1|微软开发的 Intel PCI IDE Driver<br>更改此项服务将会导致系统 **无法启动**|
|intelpmax|Intel(R) Dynamic Device Peak Power Manager Driver|3|-|1|微软开发的 Intel Power Limit Driver<br>电源限制驱动？|
|intelppm|Intel Processor Driver|3|-|1||
|iorate|Disk I/O Rate Filter Driver<br>磁盘 I/O 速率筛选器驱动程序|0|-|1|<u>为磁盘 I/O 流量提供速率控制。</u><br>更改此项服务将会导致系统 **无法启动**|
|IpFilterDriver|IP Traffic Filter Driver<br>IP 流量筛选器驱动程序|3|-|10||
|iphlpsvc|IP Helper|2|-|20|<u>使用 IPv6 转换技术(6to4、ISATAP、端口代理和 Teredo)和 IP-HTTPS 提供隧道连接。如果停止该服务，则计算机将不具备这些技术提供的增强连接优势。</u>|
|IPMIDRV||3|4|1|微软开发的 WMI IPMI 驱动，企业远程控制相关|
|IPNAT|IP Network Address Translator|3|-|1||
|IPT||2||1|待测试，Intel 处理器的调试追踪功能<sup>13</sup>|
|IpxlatCfgSvc|IP Translation Configuration Service<br>IP 转换配置服务|3|-|20|<u>配置和启用从 v4 到 v6 的转换，反之亦然</u>|
|isapnp||0|-|1|更改此项服务将会导致系统 **无法启动**<br>微软开发的 PNP ISA Bus 驱动|
|iScsiPrt|IScsiPort Driver<br>iScsiPort 驱动程序|3|-|1||
|ItSas35i||0|4|1|博通 Avago SAS Gen3.5 驱动，待测试|
|kbdclass|Keyboard Class Driver|3|-|1||
|kbdhid|Keyboard HID Driver|3|-|1||
|kdnic|Microsoft Kernel Debug Network Miniport (NDIS 6.20)<br>Microsoft 内核调试网络微型端口(NDIS 6.20)|3|-|1||
|KeyIso|CNG Key Isolation|3|-|10|<u>CNG 密钥隔离服务宿主在 LSA 进程中。如一般原则所要求，该服务为私钥和相关加密操作提供密钥进程隔离。该服务在与一般原则要求相一致的安全进程中存储和使用生存期长的密钥。</u><br>参见 **CNG**|
|KSecDD||0|-|1|微软开发的 Kernel Security Support Provider 接口<br>更改此项服务将会导致系统 **无法启动**|
|KSecPkg||0|-|1|微软开发的 Kernel Security Support Provider 接口<br>更改此项服务将会导致系统 **无法启动**|
|ksthunk|Kernel Streaming Thunks|3|-|1|音视频流媒体支持|
|KtmRm|KtmRm for Distributed Transaction Coordinator|3|-|20|<u>协调分布式事务处理协调器(MSDTC)和内核事务管理器(KTM)之间的事务。如果不需要，建议保持该服务的停止状态。如果需要，MSDTC 和 KTM 将自动启动该服务。如果此服务已禁用，任何与内核资源管理器交互的 MSDTC 事务将失败，并且任何显式依赖它的服务将无法启动。</u>|
|LanmanServer|Server|2|-|20|<u>支持此计算机通过网络的文件、打印、和命名管道共享。如果服务停止，这些功能不可用。如果服务被禁用，任何直接依赖于此服务的服务将无法启动。</u>|
|LanmanWorkstation|Workstation|2|-|20|<u>使用 SMB 协议创建并维护客户端网络与远程服务器之间的连接。如果此服务已停止，这些连接将无法使用。如果此服务已禁用，任何明确依赖它的服务将无法启动。</u>|
|lfsvc|Geolocation Service|3|4|20|<u>此服务将监视系统的当前位置并管理地理围栏(具有关联事件的地理位置)。如果你禁用此服务，应用程序将无法使用或接收有关地理位置或地理围栏的通知。</u>|
|LicenseManager|Windows License Manager Service<br>Windows 许可证管理器服务|3|-|20|<u>为 Microsoft Store 提供基础结构支持。此服务按需启动，如果禁用此服务，则通过 Microsoft Store 获得的内容将无法正常运行。</u>|
|lltdio|Link-Layer Topology Discovery Mapper I/O Driver<br>链路层拓扑发现映射器 I/O 驱动程序|2|-|1||
|lltdsvc|Link-Layer Topology Discovery Mapper|3|-|10|<u>创建网络映射，它由电脑和设备拓扑(连接)信息以及说明每个电脑和设备的元数据组成。如果禁用此服务，则网络映射将不能正常工作。</u>|
|lmhosts|TCP/IP NetBIOS Helper|3|-|20|<u>提供 TCP/IP (NetBT) 服务上的 NetBIOS 和网络上客户端的 NetBIOS 名称解析的支持，从而使用户能够共享文件、打印和登录到网络。如果此服务被停用，这些功能可能不可用。如果此服务被禁用，任何依赖它的服务将无法启动。</u>|
|LSI_SAS||0|4|1|LSI Fusion-MPT SAS 驱动|
|LSI_SAS2i||0|4|1|LSI SAS Gen2 驱动|
|LSI_SAS3i||0|4|1|博通 Avago SAS Gen3 驱动|
|LSI_SSS||0|4|1|LSI SSS PCIe/Flash|
|LSM|Local Session Manager|2|-|20|<u>管理本地用户会话的核心 Windows 服务。停止或禁用此服务将导致系统不稳定。</u>|
|luafv|UAC File Virtualization|2|-|2|<u>虚拟化每个用户位置的文件写入失败。</u>|
|LxpSvc|Language Experience Service<br>语言体验服务|3|-|20|<u>为部署和配置 Windows 本地化资源提供基础结构支持。此服务将按需启动，如果禁用，其他 Windows 语言将不会部署到系统，Windows 可能无法正常工作。</u>|
|MapsBroker|Downloaded Maps Manager|2|4|10|<u>供应用程序访问已下载地图的 Windows 服务。此服务由访问已下载地图的应用程序按需启动。禁用此服务将阻止应用访问地图。</u>|
|mausbhost|MA-USB Host Controller Driver<br>MA-USB 主机控制器驱动程序|3|-|1||
|mausbip|MA-USB IP Filter Driver<br>MA-USB IP 筛选器驱动程序|3|-|1||
|SecurityHealthService|Windows 安全中心服务|3|4|10|<u>Windows 安全中心服务处理统一的设备保护和运行状况信息</u><br>Windows Defender 相关，建议禁用|

#### 其他查找不到信息的未知服务

|服务名称<sup>1</sup>|显示名称 (EN)<sup>2</sup>|默认启动类型|优化后启动类型<sup>3, 4</sup>|服务类型<sup>5</sup>|备注<sup>6</sup>|
|----|----|----|----|----|----|
|amdgpio2|AMD GPIO Client Driver<br>AMD GPIO 客户端驱动程序|3||1|<u></u>|
|amdi2c|AMD I2C Controller Service<br>AMD I2C 控制器服务|3||1|<u></u>|
|AmdK8|AMD K8 Processor Driver|3||1||
|AmdPPM|AMD Processor Driver|3||1||
|amdsata||0||1||
|amdsbs||0||1||
|amdxata||0||1||

1. 该服务在 *注册表 (Regedit.exe)* 中的 *键名*
2. 该服务在 *服务 (services.msc)* 中的 *显示名称*
3. `-` 代表不建议优化，或默认为 *手动* 无需优化
4. 优化建议仅针对非公司环境的个人电脑
5. 该值为 *注册表 (Regedit.exe)* 中的 **16 进制** 值(打开值编辑时的默认选项)
6. 资料来源为 [batcmd](https://batcmd.com/windows/10/services/) 、 [Revert Service](https://revertservice.com/10/) 以及个人实机测试
7. 带下划线的为 **Microsoft官方中文描述** (GitHub 不支持显示下划线)
8. 禁用 Windows Update 相关后，无法从 Microsoft Store 安装和更新应用，但你可以通过 [Microsoft Store - Generation Project (v1.2.3) \[by @rgadguard & mkuba50\]](https://store.rg-adguard.net) ，来下载想要安装应用的 Appx 软件包进行本地安装
9. 该服务无描述，官方描述取自 [Microsoft 在线文档](https://learn.microsoft.com/zh-cn/windows/win32/seccng/cng-features)
10. 该服务无描述，参考链接 [file.net](https://www.file.net/process/compositebus.sys.html)
11. 描述节取自 [Microsoft 在线文档](https://learn.microsoft.com/en-us/windows/compatibility/desktop-activity-moderator)
12. 参考链接 [serverfault](https://serverfault.com/questions/829782/what-exactly-is-the-data-sharing-service-in-windows-server-2016)
13. 参考链接 [GitHbu](https://github.com/ionescu007/winipt)

[上一级](../README.md)

[笔记首页](../../../README.md)