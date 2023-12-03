# Steam 游戏疑难杂症什锦

### Half-Life: Alyx

游戏总是提示:

```
SteamVR runtime failure!

Timed out waiting for response from Mongoose.
SteamVR needs to be restarted.
```

头显中能看到游戏标题的背景场景，但是菜单无法显示出来，且一点错误提示的 **OK** 游戏便会自动退出，重启串流驱动、SteamVR、Steam、电脑均无法解决

解决方案：

在 Steam 打开游戏设置，在启动参数中加入 `-novid`，然后再启动游戏即可

### Your Diary +

DMM JP 上的 R18 补丁: [链接](https://dlsoft.dmm.co.jp/detail/cuffs_0022/) <sub>( 仅适用于中英文版本 )</sub>

#### 在 SteamOS 上游玩需要执行的操作

1. 下载 *GE-Proton7-43* ，并把它设置为游戏的兼容性工具
2. 在 Steam 中运行一次游戏<br><sub> ( 游戏会出错，不需要担心，这一步我们只是为了让 Steam 创建该游戏的 Proton 环境而已 )</sub>
3. 安装 Protontricks<br><sub>安装方法查考: [GitHub](https://github.com/Matoking/protontricks) 或 [Flathub](https://flathub.org/apps/details/com.github.Matoking.protontricks)</sub>
4. 打开你的代理软件，因为要安装的 wine 功能需要连接到外网获取<br>同时确保已在终端中运行代理设置命令 ( `export https_proxy ......` )
5. 终端运行 `flatpak run com.github.Matoking.protontricks --gui`
   1. 选择 *Your Diary + : 761700* → *OK*
   2. 选择 *Select the default wineprefix* → *OK*
   3. 选择 *Run winecfg* → *OK*
   4. 在 *Wine configuration* 的 *Applications* 标签中，把 *Windows Version* 改为 *Windows 7* ，然后点击 *Apply* → *OK*
   5. 一直点击 *Cancel* ，直到完全退出 Protontricks
6. 终端运行 <br> `flatpak run com.github.Matoking.protontricks 761700 quartz` <br><sub>( 请确保你的代理设置正确，否则无法成功安装这个功能 )</sub>
7. 终端运行 <br> `flatpak run com.github.Matoking.protontricks 761700 lavfilters` <br>安装时请确保勾选了所有的组件<br><sub>( 请确保你的代理设置正确，否则无法成功安装这个功能 )</sub>
8. 在 Steam 客户端中打开游戏设置，并把 `LANG=ja_JP.UTF-8 %command%` 填入启动参数
9. 开始愉快地游玩

---

[上一级](../README.md)

[笔记首页](../../README.md)