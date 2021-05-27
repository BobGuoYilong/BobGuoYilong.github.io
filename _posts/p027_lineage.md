---
layout: post
author: Bob Guo
title: 既然能Root为什么不能吃AOSP
subtitle: 华硕P027平板移植AOSP记录
date: 
tags: Android 平板 移植
published: false  #write true to publish this article.
---
最近买到了一台Pixel C，之前用的华硕P027平板就可以空下来折腾了。这台平板是可以解锁并Root的，但华硕官方的系统停在了Android 7.0,而且UI本身也并不符合我的使用习惯。正好最近又把放在公司写稿的机器装成了Arch Linux,就来折腾一下看看能不能把这倒霉催玩意儿适配一下AOSP。
# 平板
这台平板的产品名叫做ZenPad 3S 10,有四个版本：国行的P027、国际版的Z500M以及Z500KL和Verizon特供的ZT500KL。前两个版本都只支持WiFi,后两个版本都支持4G。在配置上，前两者采用了MTK 8176方案，后两者采用了骁龙650方案，其他参数对于搞适配来说意义不大在此不表。我手上的机器是国行的P027,通过[这个](https://forum.xda-developers.com/t/root-magisk-for-asus-zenpad-10-3s-p027.3681783/)XDA上的教程刷成了国际版Z500M的固件，并成功刷入TWRP和Magisk。  
MediaTek MT8176这颗SoC采用28nm HPM工艺，有两个2.1Ghz的A72和四个1.7Ghz的A53核心，GPU是Imagination Technology的PowerVR GX6520，对于我的需求（看片上网）绰绰有余，但如果要拿它打游戏那可能还不太现实。同样使用这一方案的还有小米平板3,这点倒是给我做适配多增添了一点信心。  
# 准备
这台平板的内核源代码可以从[华硕的官方网站](http://dlcdnet.asus.com/pub/ASUS/EeePAD/Zenpad/Z500M/Z500M_V13_6_10_15_kernel.zip)下载；最新版官方系统包也可以找到；AUR有一个包可以自动安装所有需要的依赖；下载AOSP源码这种也不用什么教程。整理完这些东西就可以开始动手了。  
我编译的平台是我的R7 1700X桌面电脑，大致配置如下：
>                   -`                    bob@PegionFishLinuxStation 
>                  .o+`                   -------------------------- 
>                 `ooo/                   OS: Arch Linux x86_64 
>                `+oooo:                  Kernel: 5.10.38-1-lily 
>               `+oooooo:                 Uptime: 3 hours, 43 mins 
>               -+oooooo+:                Packages: 1548 (pacman) 
>             `/:-:++oooo+:               Shell: bash 5.1.8 
>            `/++++/+++++++:              Resolution: 3840x2160 
>           `/++++++++++++++:             DE: Plasma 5.21.5 
>          `/+++ooooooooooooo/`           WM: KWin 
>         ./ooosssso++osssssso+`          Theme: Breeze Dark [Plasma], Breeze [GTK2/3] 
>        .oossssso-````/ossssss+`         Icons: breeze-dark [Plasma], breeze-dark [GTK2/3] 
>       -osssssso.      :ssssssso.        Terminal: konsole 
>      :osssssss/        osssso+++.       CPU: AMD Ryzen (16) @ 3.400GHz  
>     /ossssssss/        +ssssooo/-       GPU: NVIDIA GeForce GTX 960  
>                                                    Memory: 9686MiB / 32093MiB   

我的工作目录放在/home/bob/Desktop/nougat，接下来所有的命令都在这个目录下进行。  
我的发行版是Arch Linux,通过安装AUR中的[Lineageos-devel](https://aur.archlinux.org/packages/lineageos-devel/)包自动安装了全部的依赖，如果你使用其它的发行版就需要自己查询需要安装哪些软件包了。  
除了AOSP源码和Kernel之外，还需要从最新的UL-P027-WW-14.0210.1806.33-user ROM包中提取必要的数据。但是，把文件下载下来之后，解压出来的并不是我们熟悉的img,而是一个system.new.dat文件。为了提取vendor和驱动，就需要从这个dat文件中提取资料。使用[sdat2img](https://github.com/xpirt/sdat2img)这个开源项目可以提取出img文件，然后就可以从img文件中提取出
# 正式编译