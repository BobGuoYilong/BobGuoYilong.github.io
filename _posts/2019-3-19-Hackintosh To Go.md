---
layout: post
title: 打造个人开发环境（1）
subtitle: 将macOS High Sierra开发环境迁移到移动U盘中
tags: 黑苹果 Hackintosh macOS Arch 迁移 OS
published: true
---

   众所周知，作为一个C程序员兼Linux爱好者，我对GNU/Linux开发环境是极为欣赏的。但是，作为一个内容创作者，我也不得不使用包括Adobe Premiere Pro在内的一系列软件。所以，为了折中，我在我的电脑上安装了Hackintosh，具体来说，是macOS High Sierra。不过，它毕竟是一个非自由软件，而且说实话，黑苹果体验也确实并不完美。所以，我打算把整个黑苹果的开发环境迁移到我的128G自制移动固态硬盘上，而我的实体机，为了能够方便地进行一些开发编译，将会改为安装Arch Linux。  
   首先，先介绍一下这个DIY的固态硬盘。![NGFF尺寸的固态即使装在固态盒里也很小巧]({{site.baseurl}}/https://github.com/BobGuoYilong/BobGuoYilong.github.io/blob/master/img/Hacintosh%20To%20Go/ssd1.jpg)我的戴尔平板是128G的版本，到手之后，我很快就买了一个256G的PM981，而更换下来的128G SC308旧开始吃灰。于是，我买了一个硬盘盒，将它改造成了一个移动SSD。![USB-C接口，这东西就是未来]({{site.baseurl}}/https://github.com/BobGuoYilong/BobGuoYilong.github.io/blob/master/img/Hacintosh%20To%20Go/ssd2.jpg)它做移动SSD可以说是相当合适了，发热不高，速度不快不至于让USB3溢出，M.2 NGFF让它足够小巧玲珑，可以随身携带。我个人相当中意它改造成移动SSD之后的样子。![一些数据，来源macOS磁盘工具]({{site.baseurl}}/https://github.com/BobGuoYilong/BobGuoYilong.github.io/blob/master/img/Hacintosh%20To%20Go/ssd3.jpg)  
   OK，我已经预先准备好一个Arch系统盘，![虽然是USB2.0的盘子但是还不是很差]({{site.baseurl}}/https://github.com/BobGuoYilong/BobGuoYilong.github.io/blob/master/img/Hacintosh%20To%20Go/arch.jpg)接下来只需要先把macOS安装到SSD里即可。P750DM2的bios键是f2，进入BIOS确定系统设置都正常之后，从安装盘启动。  
进入启动盘，一切跟安装一般的macOS设备没有什么区别，只是注意抹掉和安装的磁盘是哪个。![选择磁盘格式]({{site.baseurl}}/https://github.com/BobGuoYilong/BobGuoYilong.github.io/blob/master/img/Hacintosh%20To%20Go/wipe_ssd.jpg)![抹盘中]({{site.baseurl}}/https://github.com/BobGuoYilong/BobGuoYilong.github.io/blob/master/img/Hacintosh%20To%20Go/wiping.jpg) 我的两个2T机械硬盘，一个是NTFS协议，一个是Apple专有分区协议。显然，它们都不是Linux环境下的最优解。幸好，Apple专有协议的那块硬盘里面只有我需要用的备份文件，所以在恢复完开发环境之后我就要把那个盘抹掉。![抹去完成]({{site.baseurl}}/https://github.com/BobGuoYilong/BobGuoYilong.github.io/blob/master/img/Hacintosh%20To%20Go/wipe_complete.jpg)   
进入安装macOS的界面![启动到安装盘，注意选择]({{site.baseurl}}/https://github.com/BobGuoYilong/BobGuoYilong.github.io/blob/master/img/Hacintosh%20To%20Go/boot_to_install.jpg) ，请记住要选择的是哪一个盘。我机器内置的SM961和这个固态都被命名为macOS，不过内置硬盘和外置硬盘是不同的图案，一般人不会弄错。![选择安装到的磁盘]({{site.baseurl}}/https://github.com/BobGuoYilong/BobGuoYilong.github.io/blob/master/img/Hacintosh%20To%20Go/install_to.jpg)   
选择确认，接下来就是漫长的等待。![安装中，可能是因为USB3+SATA的原因，速度有点慢]({{site.baseurl}}/https://github.com/BobGuoYilong/BobGuoYilong.github.io/blob/master/img/Hacintosh%20To%20Go/installing.jpg)  
明天继续，接下来就可以把备份文件转移进去了。  
