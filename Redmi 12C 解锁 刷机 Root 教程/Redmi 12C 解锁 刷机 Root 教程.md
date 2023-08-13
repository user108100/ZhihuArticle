> 买了 Redmi 12C 还要什么自行车 当入门机用用不错的  
> 需要用到的东西，如果是文件，建议临时放在一个文件夹，不要放桌面搞乱了  
> 部分文件的获取需要法力加持，嘿嘿嘿  

---

# 声明  
## 创作立场  
本人并不满足于官方提供的标准功能，于是就开始搞机，试试刷入 Root，成功后就有了本文  

## 风险警告  
刷机有风险，操作需谨慎  
实际操作导致实际损失的，本人概不负责  

# 需要用到的东西  
0. 脑子  
1. Redmi 12C 手机  
2. Windows10 电脑  
3. MiFlash（线刷工具）  
	https://roms.miuier.com/zh-cn/tools/  
	https://xiaomirom.com/download-xiaomi-flash-tool-miflash/  
	https://miuiver.com/miflash/  
4. MiFlashUnlock（解锁 BL 工具）  
	https://www.miui.com/unlock/download.html  
	https://miuiver.com/miunlock/  
5. Redmi 12C 线刷包  
	https://roms.miuier.com/zh-cn/devices/earth/  
	https://xiaomirom.com/rom/redmi-12c-earth-china-fastboot-recovery-rom/  
	https://miuirom.org/phones/redmi-12c  
	https://xiaomifirmwareupdater.com/miui/earth/  
	https://miuiver.com/tag/earth-stable-rom/  
6. 安卓 platform-tools（包含 adb, fastboot 等工具）  
	https://developer.android.google.cn/studio/releases/platform-tools?hl=zh-cn  
	https://developer.android.google.cn/studio/command-line/adb?hl=zh-cn  
7. Magisk 安装包  
	https://github.com/topjohnwu/Magisk/releases  
8. boot.img 文件  
	在线刷包文件夹中的images文件夹里，到时候复制到手机里  

# 可以选择安装的东西  
1. Shizuku（方便地使用 Root 权限）  
	https://www.coolapk.com/apk/moe.shizuku.privileged.api  
	https://github.com/RikkaApps/Shizuku/releases  
	https://apt.izzysoft.de/fdroid/index/apk/moe.shizuku.privileged.api  
	https://shizuku.rikka.app/zh-hans/download/  
2. MT 管理器（方便地操作文件）  
	https://www.coolapk.com/apk/bin.mt.plus  
	https://mt2.cn/download/  
3. TWRP（方便玩机）  
	https://xiaomitools.com/download/redmi-12c-twrp/  
	https://xiaomitools.com/download/?pack=0307fec2cef6aec340b8426490977ef0  
	https://secyukle.com/dosya/uploads/twrp/twrp-12.1_3.7.0-v000-earth-20230629.rar  

# 怎么做  

## 先妥善处理好手机上的数据  
备份好数据，方式多样，自己搜索  

## 进 fastboot 模式 的方法  
首先把手机关机，然后同时按住【电源键】和【音量下键】  
多试几次，你就能进入一个界面，正中心有【FASTBOOT】字样  

## 解锁 BL  
先去手机设置 我的设备 全部参数与信息 然后连续戳【MIUI 版本】字样，打开开发者模式  
然后去手机设置 更多设置 开发者选项 设备解锁状态 按要求绑定账号和设备    
> 这时候你可以顺手把【USB 调试】打开和【默认 USB 配置】调为 【传输文件（MTP）】，方便传输文件  

在电脑上打开 MiFlashUnlock，然后登录，先安装驱动，然后按要求解锁即可  
一般情况下你要等上7天，网上的秒解锁我没试过  

## 操作 adb, fastboot 的方法  
用数据线连接手机和电脑，确保【USB 调试】已经开启  
解压 platform-tools 到一个目录，进入这个目录  
在路径栏输入【cmd】然后回车，此时出现了 cmd 窗口，cmd 的路径为本目录  
> 可以把文件直接拖动到 cmd 窗口，然后文件路径就粘贴到 cmd 窗口中了  

然后就可以输入命令操作 adb 了  

## 电脑与手机 文件传输 的方法  

### adb 法  
手机上文件的路径，举个例子 `/sdcard/hello.txt` `/storage/emulated/0/hello.txt`  两种表述，都指向同一个文件，在内部储存根目录的 `hello.txt`  
> 执行 adb 命令前，可以先使用 `adb devices` 看看设备列表，有就是可以调试，同时注意看手机上有没有对话框提示，点同意就行了  

- 如果电脑文件要传到手机  
在 cmd 窗口输入命令 `adb push 【电脑上文件的路径】【空格】【手机上文件的路径】` 然后稍等，文件大概以 20mb/s 的速度传输  
- 如果手机文件要传到电脑  
两个路径对调一下，然后 `adb push` 改为 `adb pull` 即可  

### MTP 法  
在电脑桌面双击【此电脑】可以看到标着手机型号的字样，双击进去，像在 Windows 一样复制粘贴文件吧  

## 线刷刷入  
解压下载好的线刷包，复制它的路径，注意路径不能有空格  
> 如果不想刷完后，BL 锁又锁上，建议删掉线刷包文件夹里带【lock】字样的批处理脚本，避免手残  

打开 MiFlash ，可以粘贴路径到路径框，也可以手选  
先安装驱动，可以点菜单栏的【Driver】，或者它自动提示  
接下来用数据线连接手机和电脑，然后点击【加载设备】  
> 注意右下角，如果不想刷完后，BL 锁又锁上，那么选择【全部删除】或【保留用户数据】（保留用户数据我没试过）  

最后点击【刷机】，就能开始刷入，大概等上5分钟就好  
等它10分钟左右，就可以开始配置新机  

## 安装 Magisk 以解锁 Root  
在手机安装好 Magisk，可以选择安装 MT 管理器，Shizuku  
在手机放好 boot.img 文件  
进入 Magisk，在【Magisk】字样右边点【安装】  
选择【选择并修补一个文件】然后选择刚刚放好的 boot.img  
文件修补好后，把文件复制到电脑上  
然后让手机进入 fastboot 模式，开始操作adb，执行命令  
`fastboot flash boot 【修补好的boot.img】`   
> 这时候可以顺便刷入 TWRP   
> 执行命令 `fastboot flash recovery 【TWRP文件的路径】`  
> 如果不想刷入，只是临时启动，那么换成  
> `fastboot boot 【TWRP文件的路径】`  
> 然而我用了一下命令才刷入了 TWRP  
> `fastboot flash boot 【TWRP文件的路径】`  
> 貌似我找的 TWRP 不太对？还是我搞错了使用方法？  

命令执行完后，重启手机，然后享受你的 Root 权限吧  

# 最后的话  
初期写文，经验浅显，请读者多多见谅  
偷懒不插图，嘿嘿嘿  
TWRP 我找了大半天，最后在谷歌搜到了  
好像解锁 Root 前不用刷机的，读者可以自己探索一下  
