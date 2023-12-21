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


## 调整 Log 的时间显示格式<sup>[2]</sup>

```shell
git config --global alias.lg "log --date=format-local:'%Y-%m-%d %p %I:%M:%S"
```

以上命令是通过 Git 本身的别名功能 <sub>(alias)</sub> 来把 `lg` 映射为带了指定时间格式参数的 `log`

调整后的时间格式为：`年-月-日 上午 时:分:秒` ，小时为 12 小时制

时间格式的具体含义，可以参考引用来源的链接

> Git 的 *alias* 无法像 Shell 里面的一样直接替换原本就存在的关键词，例如把 `log` 映射成 `log --date=format-local:'%Y-%m-%d %H:%M:%S'` ，这种设置是不生效的，你必须指定一个新的关键词来进行映射

## 引用来源：

1. [How to pull into multiple branches at once with git?](https://superuser.com/questions/623217/how-to-pull-into-multiple-branches-at-once-with-git)

2. [How to change Git log date formats](https://stackoverflow.com/questions/7853332/how-to-change-git-log-date-formats)

---

[上一级](../README.md)

[笔记首页](../../README.md)