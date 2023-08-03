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

---

[上一级](../README.md)

[笔记首页](../../README.md)