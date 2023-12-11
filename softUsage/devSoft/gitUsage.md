# Git 使用技巧

## 使用一条命令同时把所有分支 pull 到最新版本 <sup>[1]</sup>

```shell
git fetch --update-head-ok origin 远程分支1:本地分支1 远程分支2:本地分支2
```

示例输出：

```shell
> git fetch --update-head-ok origin main:main master:master hugo:hugo
remote: Enumerating objects: 116, done.
remote: Counting objects: 100% (116/116), done.
remote: Compressing objects: 100% (70/70), done.
remote: Total 77 (delta 41), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (77/77), 14.48 KiB | 110.00 KiB/s, done.
From /mnt/disk2/GitHub/personal_note
 * [new branch]      main       -> main
 * [new branch]      master     -> master
   03eac90..91c2bb6  main       -> origin/main
```

## 从整个仓库的所有版本里彻底删除某个文件

> ⚠ 下面的命令必须在仓库的根目录下执行

```shell
git filter-branch --force --index-filter "git rm --cached --ignore-unmatch 你要彻底删除的文件路径(从仓库根目录开始)" --prune-empty --tag-name-filter cat -- --all
git push --all --force
```

## 引用来源：

1. [How to pull into multiple branches at once with git?](https://superuser.com/questions/623217/how-to-pull-into-multiple-branches-at-once-with-git)

---

[上一级](../README.md)

[笔记首页](../../README.md)