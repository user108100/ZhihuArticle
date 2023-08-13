> **吐槽**:  
> 本人有一款 锐族 X02 MP3 播放器，发现它支持播放avi和amv两种格式的视频  
> 于是就想使用 ffmpeg 把视频转为它可以播放的形式  
> 根据网友反馈，格式工厂是无法转换成功的  
> 而 MP3 中自带的转换工具使用方法过于鸡肋  
> 经过一番琢磨后成功，就有了本文  
---
> **不得不说的废话**：  
> 现在假设 你是一个人  
> 拥有 逐字阅读 本文 和 其他网站 的能力  
> 基本懂得使用 Windows10 操作系统  
> 懂得文件的 复制 粘贴 压缩 解压 和 文本的 输入 复制 粘贴  
> 懂得使用拥有图形化界面的工具
> 不熟悉 命令行工具 的 使用方法
> 不熟悉 代码 和 开发 等领域  
> 不熟悉 如何运用法力 访问国内难以访问的网页  
> 鄙人会尝试 用文字 手把手 教会你 本文所讲  
---
# 配置 ffmpeg  
这个在另一篇文章讲得很明白了  

# 执行 ffmpeg 命令  
`ffmpeg -i 【原视频的路径】 -c:v amv -c:a adpcm_ima_amv -pix_fmt yuvj420p -strict -1 -s 160x120 -ar 22050 -ac 1 -r 30 -block_size 735 -q 0 【转换后视频的路径】`  
在这个命令中 `-s 160x120` 表示转换后视频的分辨率  

# 方便地使用  

本人写了个批处理脚本  

```
@echo off
set "path=%~dp0"
cd /d "%path%"

set "ffmpegexe=ffmpeg.exe"
set "modecom=C:\Windows\System32\mode"

echo path: %path%
echo ffmpeg: %ffmpegexe%
:loop1

echo.
set /p "url=URL: "
set /p "name=Name: "

start "Name: %name%" cmd /k "%modecom% con cols=36 lines=10 & %ffmpegexe% -hwaccel cuda -i %url% -c:v amv -c:a adpcm_ima_amv -pix_fmt yuvj420p -strict -1 -s 160x120 -ar 22050 -ac 1 -r 30 -block_size 735 -q 0 %path%%name%.amv"

goto loop1
rem convert to amv: https://superuser.com/questions/1649146/convert-mpeg4-to-amv-via-ffmpeg
rem ffmpeg -i a.avi -c:v amv -c:a adpcm_ima_amv -pix_fmt yuvj420p -strict -1 -s 160x120 -ar 22050 -ac 1 -r 30 -block_size 735 -q 0 a.amv
pause
```

## 保存为批处理脚本  
如图，仔细地按箭头点，把以上代码粘贴过去即可  
![[mp3 播放器 ffmepg 转换 视频 为 amv/1.png]]  

## 使用脚本  
如图，跟着箭头点  
在脚本窗口中先输入原视频路径，回车，再输入转换后视频的名字，就会转换视频到同目录  
![[2.脚本使用方法.png]]  

# 最后的话  
参考链接，表示感谢：[Convert MPEG4 to AMV via ffmpeg](https://superuser.com/questions/1649146/convert-mpeg4-to-amv-via-ffmpeg)  
会改批处理的读者可以自行修改，让其更易使用  
