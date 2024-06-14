# 多媒体软件指南

## ImageMagick

将图片以多个文件名顺序转换为 PDF 文件，并设置临时的缓存目录

当使用 Adobe Acrobat 或其他 PDF 编辑器创建 PDF 文件时，它们很可能都会强制压缩你的图片质量，并且要求必须将分辨率转换为为常见的纸张大小

而就 Acrobat 来说，如果导入了太多图片后，还会提示「文件太大，无法保存」

为了解决这些问题，你可以选择用 [ImageMagick](https://imagemagick.org) 来把图片转换为 PDF 文件， ImageMagick 不存在上述的限制

下面列出一个用例，该用例是在 Windows 下进行演示，目的是把 `D:\Input` 里面所有的 `jpg` 文件 **<i>保留原始分辨率且无损</i>** 转换为 `D:\output.pdf`

`convert.exe -define registry:temporary-path=C:\temp -quality 100 D:\Input\*.jpg D:\output.pdf`

参数解释：

+ `registry:temporary-path=C:\temp`
   > 把临时缓存目录设置为 `C:\temp` <br> 当 ImageMagick 工作时，会为每一个输入文件都创建一个对应的临时文件 <br> 对于 Windows 来说一般是位于 `%AppData%` 里 <br> 如果你的用户目录所在的磁盘空间不足，可以使用本参数，指定一个别的位置
+ `-quality 100`
   >指定转换的质量， `100` 为最高质量

## FFmpeg

将 gif 输出成序列帧: `ffmpeg.exe -i path\to\input.gif path\for\output\frame_%d.png`

> 其中 `-i` 参数指定的文件为输入文件，避免产生输入输出方向错误，建议加上
>
> 输出文件名中的 `%d` 可以让输出的每一帧图片文件名带上数字序号

---

[上一级](../README.md)

[笔记首页](../../README.md)
