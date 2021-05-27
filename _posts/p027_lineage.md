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
# 第一步：