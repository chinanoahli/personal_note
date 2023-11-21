---
title: "Nintendo Switch SXOS 转 Atmosphere"
date: 2023-02-25T10:58:40+08:00
draft: false
---

# Nintendo Switch SXOS 转 Atmosphere

> 本教程不包含两个系统之间的虚拟系统互相转换教程，请转换前备份好各个游戏的存档
>
> SXOS生成的虚拟系统无需保留，因为要将其转换成Atmosphère能用的并不容易，建议删掉后重新使用 **hekate - Nyx** 创建虚拟系统

1. 请先备份好所有你SXOS的启动文件以及许可证和启动文件，因为SXOS已经倒闭，其官网也无法再进入，一旦遗失你的许可证，你就永远无法再启动SXOS了

    相关文件如下：

   1. boot.dat    →    SXOS本体
   2. **license.dat**    →    SXOS许可证，无论如何，请一定要备份好此文件
   3. license-request.dat    →    用于在SXOS官网重新下载许可证的文件，鉴于官网已经关停，所以可不备份此项

2. 如果你曾经将虚拟系统安装到机器的自带储存里面的话，请现在将虚拟系统移动到内存卡

3. 下载 SX Gear：[下载地址 (需要翻墙)](https://web.archive.org/web/20210217231219/https://sx.xecuter.com/download/SX_Gear_v1.1.zip)

   > 这个工具允许SX硬破芯片加载不是由SX团队开发的第三方payload
   >
   > 如果你无法翻墙，可以直接点击下面的文件下载
   >
   > [SX_Gear_v1.1.zip](https://github-share-1304366332.cos.ap-guangzhou.myqcloud.com/game/nintendo/switch/attachments/SX_Gear_v1.1.zip)

4. 下载 hekate - Nyx 破解引导程序：[下载地址](https://github.com/CTCaer/hekate)

    进入网页后，点击页面右侧的**Releases**，在弹出的页面中，下载第一个**Assets**下面的**hekate_ctcaer_X.X.X_Nyx_X.X.X.zip**

   > X.X.X 为版本号，下载最新的就行，下同

5. 下载 Atmosphère 自制系统：[下载地址](https://github.com/Atmosphere-NX/Atmosphere)

   > 下载方法同第4步
   >
   > 这里需要注意一下，除了下载 **atmosphere-X.X.X-master-XXXXXXXXX+hbl-X.X.X+hbmenu-X.X.X.zip** 以外，还需要下载 **fusee.bin**

6. 下载 Signature Patches 签名补丁：

   ~~GitHub仓库：[下载地址](https://github.com/ITotalJustice/patches)~~

   > 下载方法同第4步
   >
   > 签名补丁是必须下载的，否则无法安装盗版游戏
   >
   > 这里需要注意一下，这里只需要下载 **fusee.zip** 文件即可

   > 2022-09-27 Update
   >
   > 上面的地址已经失效，如果要下载签名补丁，请前往[这里(出处)](https://sigmapatches.coomer.party/)或[这里(整合站)](https://wiidatabase.de/switch-downloads/hacks/signatur-patches/)
   >
   > 解压路径参考下面 第11步，压缩包内`atmosphere`和`bootloader`文件要放对位置

7. 创建一个文件夹，这里以 **D:\\SwitchCrack** 为例，最后需要将这个文件夹的所有内容覆盖到内存卡根目录，即可完成转换（后续更新版本方法是一样的）

8. 先备份原始的SXOS相关的文件

   1. 将内存卡中的 boot.dat 复制到 D:\\SwitchCrack 中并命名为 **boot_sxos.dat**

       重命名是为了防止以外删除，当然你也可以多备份到别的几个地方

   2. 将内出卡中的 license.dat 复制到 D:\\SwitchCrack 中

       **无论如何一定要备份好本文件，请备份到多个网盘和不同的地方**

9. 按顺序将下列文件解压到 D:\\SwitchCrack ( 按顺序解压可以不用手动建立文件夹 )

   1. SX_Gear_v1.1.zip
   2. hekate_ctcaer_X.X.X_Nyx_X.X.X.zip
   3. atmosphere-X.X.X-master-XXXXXXXXX+hbl-X.X.X+hbmenu-X.X.X.zip
   4. fusee.zip

10. 将 fusee.bin 复制到 D:\\SwitchCrack\\bootloader\\payloads 并重命名为 **atmosphere-X.X.X-fusee.bin**

    > X.X.X 为 Atmosphere 的版本号，自己根据实际修改

11. **此时，你的 D:\\SwitchCrack 应该有以下的内容**

      ```
      D:\SwitchCrack
      │  boot.dat                   # SX Gear 的启动文件
      │  boot.ini                   # SX Gear 的配置文件
      │  boot_sxos.dat              # SXOS 的启动文件
      │  hbmenu.nro
      │  hekate_ctcaer_X.X.X.bin    # hekate 的 payload
      │  license-request.dat
      │  license.dat                # SXOS 的许可证文件
      │
      ├─atmosphere
      │  │  hbl.nsp
      │  │  package3
      │  │  reboot_payload.bin
      │  │  stratosphere.romfs
      │  │
      │  ├─config
      │  ├─config_templates
      │  │      exosphere.ini
      │  │      override_config.ini
      │  │      stratosphere.ini
      │  │      system_settings.ini
      │  │
      │  ├─exefs_patches
      │  │  ├─es_patches
      │  │  │      # 此处一共是21个ips文件，文件来自于 Signature Patches
      │  │  │      # 如果它更新了，可能数目就跟本文对不上了
      │  │  │      # 无需惊慌，只需要确认跟下载到的zip文件里面的数量一样就行
      │  │  │
      │  │  └─nfim_ctest
      │  │          # 此处一共是20个ips文件，文件来自于 Signature Patches
      │  │          # 如果它更新了，可能数目就跟本文对不上了
      │  │          # 无需惊慌，只需要确认跟下载到的zip文件里面的数量一样就行
      │  │
      │  ├─fatal_errors
      │  ├─flags
      │  ├─hbl_html
      │  │  └─accessible-urls
      │  │          accessible-urls.txt
      │  │
      │  └─kip_patches
      │      ├─fs_patches
      │      |      # 此处一共是43个ips文件，文件来自于 Signature Patches
      │      |      # 如果它更新了，可能数目就跟本文对不上了
      │      |      # 无需惊慌，只需要确认跟下载到的zip文件里面的数量一样就行
      │      │
      │      └─loader_patches
      │              # 此处一共是35个ips文件，文件来自于 Signature Patches
      │              # 如果它更新了，可能数目就跟本文对不上了
      │              # 无需惊慌，只需要确认跟下载到的zip文件里面的数量一样就行
      │
      ├─bootloader
      │  │  patches.ini
      │  │  update.bin
      │  │
      │  ├─ini
      │  ├─payloads
      │  │      atmosphere-X.X.X-fusee.bin    # 第10步的 fusee.bin 文件在这里
      │  │
      │  ├─res
      │  │      icon_payload.bmp
      │  │      icon_switch.bmp
      │  │
      │  └─sys
      │          emummc.kipm
      │          libsys_lp0.bso
      │          libsys_minerva.bso
      │          nyx.bin
      │          res.pak
      │          thk.bin
      │
      └─switch
             daybreak.nro
             reboot_to_payload.nro
      ```

12. 新建文件 **hekate_ipl.ini** 并放入 D:\\SwitchCrack\\bootloader，文件内容如下，注意修改`[AutoSelect]`处的 Atmosphere 版本号需要修改

    > 这个文件的意思是在 hekate 中创建 4 个启动项目 (四个项目可以根据自己需要调整排序)：
    >
    > 1. [CrackSYS] → 进入破解系统
    > 2. [EmuNAND] → 进入虚拟系统
    > 3. [AutoSelect] → 如果有虚拟系统就进入虚拟系统，没有就直接进入破解系统 (虚拟系统需要另外手动制作)
    > 4. [NormalSYS] → 进入原版非破解系统

    ```
    [config]
    autoboot=0
    autoboot_list=0
    bootwait=3
    customlogo=1
    backlight=100
    autohosoff=0
    autonogc=1

    [CrackSYS]
    fss0=atmosphere/package3
    kip1patch=nosigchk
    atmosphere=1
    emummc_force_disable=1
    icon=bootloader/res/icon_switch.bmp

    [EmuNAND]
    fss0=atmosphere/package3
    kip1patch=nosigchk
    emummcforce=1
    atmosphere=1
    icon=bootloader/res/icon_switch.bmp

    [AutoSelect]
    payload=bootloader/payloads/atmosphere-X.X.X-fusee.bin
    icon=bootloader/res/icon_switch.bmp

    [NormalSYS]
    fss0=atmosphere/package3
    emummc_force_disable=1
    stock=1
    icon=bootloader/res/icon_switch.bmp
    ```

13. 新建文件夹 **D:\\SwitchCrack\\atmosphere\\hosts** 并在其中新建下列三个文本文件：

    1. default.txt
    2. sysmmc.txt
    3. emummc.txt

    并写入如下内容 (三个文件内容一样)：

    ```
    # Nintendo telemetry servers
    127.0.0.1 receive-%.dg.srv.nintendo.net receive-%.er.srv.nintendo.net
    127.0.0.1 *nintendo.*
    127.0.0.1 *nintendoswitch.*
    127.0.0.1 *nintendo-europe.com
    127.0.0.1 *nintendoswitch.com.cn
    207.246.121.77 *conntest.nintendowifi.net
    207.246.121.77 *ctest.cdn.nintendo.net
    ```

    即可屏蔽所有主机与任天堂网络服务的连接 **（仅在自制系统中生效）**

14. 打开 D:\\SwitchCrack\\boot.ini 修改成以下内容（X.X.X 替换成 hekate 的版本号）

    ```
    [payload]
    file=hekate_ctcaer_X.X.X.bin
    ```

15. 至此已经成功从 SXOS 切换到 Atmosphere，将 D:\\SwitchCrack\\ 中的所有文件，覆盖到你 Switch 内存卡的根目录下，重新开机即可

16. 常用工具下载地址 (以下皆为工具开发者的官方发布地址，可能不包含汉化版本，但可以保证绝对是最新的原版，非魔改版本)

    1. Checkpoint 存档管理：[点此下载](https://github.com/FlagBrew/Checkpoint/releases)
    2. NX-Shell 文件浏览管理工具：[点此下载](https://github.com/joel16/NX-Shell/releases)
    3. TinWoo 游戏安装工具：[点此下载](https://github.com/mrdude2478/TinWoo/releases)
    4. Awoo Installer 游戏安装工具：[点此下载](https://github.com/Huntereb/Awoo-Installer/releases)
    5. TinFoil 游戏安装工具：[点此下载](https://tinfoil.io/Download) (下载NSP版本，用TinWoo或Awoo安装即可)

17. \[非必要\]用Lockpick_RCM导出`prod.keys`</br>(此工具已被任天堂举报，现已更名为`Picklock_RCM`)

   > ~~官方仓库: [下载地址](https://github.com/shchmue/Lockpick_RCM)~~，已被老任举报
   >
   > 两个备用地址: [地址1](https://github.com/iczero/Lockpick_RCM) [地址2](https://github.com/s1204IT/Lockpick_RCM)

   > 1. 下载`Picklock_RCM.bin`并更名为`Lockpick_RCM.bin`(下载方法同第4步)
   > 2. 将该文件放到`D:\SwitchCrack\bootloader\payloads`
   > 3. 开机进入hekate引导程序后，点击最上方的`Console Info`标签
   > 4. 点击 **SoC \& HW Info** 下方的`Lockpick`按钮，然后点击`Continue`按钮
   > 5. 进入Lockpick后，选择`Dump from SysNAND`
   >    (用 `Vol +` 或 `Vol -` 键进行导航，然后按下`Power`确认选择)
   > 6. Lockpick会自动将`prod.keys`导出到`sd:\switch\prod.keys`
   > 7. 按`Power`返回上一层，然后根据需要选择重启或关机即可

18. 几个自制的启动项目图标

    覆盖到 D:\\SwitchCrack\\bootloader\\res，然后修改 hekate_ipl.ini 中的 **icon** 字段即可

    [res.7z](https://github-share-1304366332.cos.ap-guangzhou.myqcloud.com/game/nintendo/switch/attachments/res.7z)

---

[上一级](../../)

[笔记首页](/)