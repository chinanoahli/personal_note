---
title: "Linux 常用技巧"
date: 2023-05-05T19:54:13+09:00
draft: false
---

# Linux 常用技巧

## 一条命令调整文件与目录的权限 <sup>[1]</sup>

> 背景:
> 
> 偶尔会接受到来自 Windows 系统的目录与文件，但是这些文件的权限经常全部都是 `0777`，这是让人难以接受的
> 
> 以前会考虑写个脚本来遍历目录调整权限，但是脚本都没有保留，所以这次就直接谷歌了

有两个办法：

1. 通过 *find* 命令

   ```shell
   # for directories
   find /path/to/dir -type d -print0 | xargs -0 chmod 0755
   
   # for files
   find /path/to/dir -type f -print0 | xargs -0 chmod 0644
   ```

2. 通过 *chmod* 命令本身的参数控制

   ```shell
   chmod -R u+rwX,go+rX,go-w /path/to/dir
   ```

   这里主要是用到了 `-X` 参数，这个参数可以为 *目录* 自动加入 **可执行** 权限
   
   但是对于文件，它会检查文件是否符合下列条件，只有符合条件的文件才会被赋予 **可执行** 权限
   
   1. 文件本身是 *可执行文件*
   
   2. 能 *被当前用户(组)* (取决于你这个 `-X` 放在命令中的哪一段) 检索到

## 引用来源

1. [Change all files and folders permissions of a directory to 644/755](https://stackoverflow.com/questions/18817744/change-all-files-and-folders-permissions-of-a-directory-to-644-755)

---

[上一级](../..)

[笔记首页](/)