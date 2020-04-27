---
layout: post
author: Bob Guo
title: 0202年还在用32位平板是什么体验？
subtitle: Venue 8 Pro 拆机篇
date: 2020-1-5
tags: 平板 戴尔
published: true
---

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;熟悉我的人都知道，我是一个戴吹。这里的戴吹不是像课戴表一样无脑吹捧戴尔，而是在有选择的情况下优先选择戴尔的二手产品。没错，我就是戴吹垃圾佬，账户上所有的产品除了一个灵越是自己人肉美帝带回之外都是二手。那么，作为一个戴吹，自然是要搞一个戴尔的平板咯。我自己手上还有一根之前留下来的A03手写笔，那么自然而然地，我的目标就转向了戴尔的V8P平板。  
![Alt text](/img/v8p/系统信息.jpg)
*戴吹快乐机，这玩意牛逼就牛逼在所有22nm Atom的八寸板子里这玩意性能吊的一笔*  
![Alt text](/img/v8p/后壳.jpg)
*中国红，很骚气的颜色，我觉得比黑色的版本好看*  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;这个系列最早其实是戴尔的智能手机产品线。没错，戴尔做过手机，surprise，surprise。之后，这个系列慢慢开始转向平板电脑的产品线，而由于大量使用了Intel Atom处理器，自然而然地就出现了使用Windows操作系统的Pro版，而其中最经典的就是V8P这台八英寸的小钢炮了。  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;我手上的这个款式是5830，搭载一颗1.8Ghz的Intel Atom Z3740D CPU，2GB的DDR3L内存，以及32GB eMMC闪存。当然，这点闪存容量在安装Windows 10后所剩无几，这时就需要使用TF卡进行拓展了。  

![Alt text](/img/v8p/存储.jpg)
*所有的Galgame全部放在TF卡上，除了Chrome都是UWP*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;至于使用体验么，只能说中规中矩。可能是因为我接触了太多高分屏设备的原因，1280x800的分辨率在八寸的屏幕上仍然存在严重的大果粒问题，但同样也带来出众的续航和性能表现。我的使用主要是玩一些小游戏和Galgame，而这样的需求这台平板能够很好的满足。电池的寿命大约是85%左右，也能保证三到四小时的工作时间。作为娱乐平板，它暂且是满足了我的需求的。  

![Alt text](/img/v8p/大果粒.jpg)
*肉眼可见的大果粒*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;当然，这篇文章不可能就这么结束。我们来看看这个平板拆开会是什么样。拆机特别简单，只要打开卡扣就可以拆机。我这里用一片吉他拨片和一个小螺丝刀就完成了所有的拆机流程。拆开之后是这样的，18wh的电池和扬声器占据了机身很大的一个部分，而主板就放在旁边，连接着所有的设备。显示面板直接放在下面，中间并没有什么防止螺丝拧过头伤到屏幕的设计。当然，这算是为了尺寸做的必要的牺牲，我也只能保持理解。  

![Alt text](/img/v8p/拨片.jpg)
*万恶之源*

![Alt text](/img/v8p/整机一览.jpg)
*整机，已经拆除所有螺丝。拆机前请拔除TF卡与SIM卡，并第一时间拔出电池。*

![Alt text](/img/v8p/主板背部一览.jpg)
*主板背部*

![Alt text](/img/v8p/主板正面一览.jpg)
*主板正面*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;仔细看看主板，好玩的事情更多。第一眼就能看到有一个写着LTE的地方被空焊，这里是接NGFF 4G网卡的地方。如果BIOS上不做限制，理论上这里可以额外安装一个固态硬盘？如果真如此，那就好玩了-毕竟eMMC作为老旧的技术在随机读写上还是不如固态硬盘的。  

![Alt text](/img/v8p/NGFF2.jpg)
*正好在这个位置上*

![Alt text](/img/v8p/NGFF3.jpg)
*这张图是最清楚可以看见NGFF的*

![Alt text](/img/v8p/NGFF1.jpg)
*NGFF的位置在电池上方*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在写着CON4501的接口的上方是整个主板的核心-无线网卡、两个DDR3内存芯片、CPU以及eMMC存储器和BIOS芯片。由于V30的主摄即使在谷歌相机的加持下也过于弟弟，这已经是我的极限了，请各位谅解。无线网卡的型号是QCA6234x2，eMMC的型号是三星的KLMBG4GEAC，是一颗eMMC 4.5的芯片。两个内存芯片都是SK海力士的H5TC4G63AFR。  

![Alt text](/img/v8p/CPU等.jpg)
*左边是电容和IC芯片，具体型号我也看不清楚*

![Alt text](/img/v8p/DDR3L.jpg)
*两颗海力士内存*

![Alt text](/img/v8p/无线网卡.jpg)
*高通无线网卡，估计这就是@TechAcetone那天爆炸的原因吧（笑）*

![Alt text](/img/v8p/eMMC.jpg)
*三星eMMC*

![Alt text](/img/v8p/CPU等（拆除屏蔽罩）.jpg)
*CPU*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;但是查一下就知道，这是一颗4Gb的内存芯片，也就是说它只有512MB的容量。两颗这个芯片，那应该是1GB的内存，怎么做到2GB的?答案就在背面-那里也有两颗同款的内存芯片。  

![Alt text](/img/v8p/背部RAM1.jpg)
*背部的两颗DRAM*

![Alt text](/img/v8p/背部RAM2.jpg)
*型号跟正面的是同一款*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;而前置摄像头、microUSB接口、电源和音量键也在这一面上。  

![Alt text](/img/v8p/IO部分.jpg)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;没错，这就是这个板子上所有的IO。一个microUSB 2,0，一个3.5mm的耳机接口，两个摄像头，剩下的就全部是button了。  

![Alt text](/img/v8p/microUSB1.jpg)
*这个是符合USB2.0的定义的5pin*

![Alt text](/img/v8p/microUSB2.jpg)
*这张比较拉跨但是也是很清楚的*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;而这里就是我所说的好玩的地方-这玩意有足够的空间防止一个USB-C接口。  

![Alt text](/img/v8p/外壳上的预留孔.jpg)
*就算装不进去打磨一下就好了嘛*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;而且它也是符合USB2.0定义的5pin接法。也就是说，只要我有一个USB-C的接口，理论上我就可以焊上去少带一根microUSB线。多好对吧？  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;OK第一篇文章就写到这里。过几天我还会再写一个三星Tab S2的文章，那篇应该写的比这个长一点了。至于这个板子什么时候搞USBC的魔改，那得等我有那个工具了再说。头已经找到了，手上有一个坏掉的寨本上的全功能Type C。具体的使用体验问题呢，我可能要之后找时间再写  