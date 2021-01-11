---
layout: post
author: Bob Guo
title: 国产强芯
subtitle: 三星Chromebook Plus评测兼ChromeOS使用手记
date: 2020-12-23
tags: 捡垃圾 Chromebook ChromeOS ARM RK3399
header-img: https://pic1.zhimg.com/v2-54d5c4407c334f0426b162f6be218226_r.jpg?source=172ae18b
published: True #write true to publish this article.
---
# 前言
说实话，对于“国产芯片”，我个人一直是有所保留的。一来作为一个老玩家，对于汉芯、红芯（虽然这玩意是浏览器）等一系列沽名钓誉之徒的行为感到不齿以至于对所有打着国产旗号大肆宣传的科技产品来自骨子里的不信任；二来作为一名生活所迫的垃圾佬，即使对于那些真的做出成绩来的国产芯片我也难以轻松入手。而第三，现有的国产设备很多难以与我长期使用的部分海外服务无缝连接，这对于我的使用来说还是有一点麻烦的。于是，我手上的各种产品要么是Intel，要么是AMD，要么是Qualcomm，要么是Exynos，很少有来自国产企业的设备。  
不过，RK3399可不在此列。这颗被谷歌贴牌OP1拿给Chromebook用的处理器不仅有大量价格较为低廉的洋垃圾，而且性能中规中矩，更是能与我长期使用的服务无缝衔接。更令人欣喜的是，这颗芯片的内核是紧跟主线的，这也就意味着只要条件允许，ArchLinuxARM这类滚动发行版也不是问题（当然我在安装的时候遇到很多问题，more on that later)。而在这些Chromebook中，这次评测的主角-Samsung Chromebook Plus（第一代）脱颖而出。  
虽然是来自“PC业务纯粹玩玩”的三星，但由于这台机器相较于传统笔记本电脑更偏向于手机/平板，加上所有Chromebook的软件部分都由Google搞定，实在没有三星软件团队“瞎搞”的空间，配合Chromebook上少有的、支持SPen的高素质屏幕与360度转轴、双USB-C，这台机器确实称得上高端Chromebook。  
# 拆机与部件说明
拆机过程十分简单，只需要螺丝刀和翘片即可。由于机器的高度一体性，具体的过程无需多言，我就只放图了。
![bottom panel](/img/chromebook_plus/d.jpg)
![bottom panel(inside)](/img/chromebook_plus/d2.jpg)

## 总览
这台机器的内部做工还是很不错的。高度集成、做工精良，确实是高端笔记本电脑的水准。
![Overview](/img/chromebook_plus/overall.jpg)
![Everyting except for speakers d-board and buttons](/img/chromebook_plus/everything.jpg)
![speakers and daughter board](/img/chromebook_plus/speaker.jpg)
![volume and power](/img/chromebook_plus/button.jpg)
![Thickness(Compare to ThinkPad T430)](/img/chromebook_plus/thick.jpg)
## 屏幕
![Display panel](/img/chromebook_plus/b.jpg)
屏幕是这台机器的一个亮点。使用2400x1600分辨率，3:2的IPS触屏，支持SPen和360度旋转，加上RK3399原生arm64架构，这台Chromebook也是一台完美的Android 9平板。当然，这里的完美要打引号。这块LQ123P1JX31面板由于拥有100%sRGB色域，在浏览多媒体内容的时候十分舒适，且由于B面全玻璃贴合工艺也不会出现传统IPS的漏光问题。鉴于ChromeOS上专业内容创作应用压倒性的稀缺，我个人觉得这块屏幕已经足够优秀。  
## 键盘和触摸板
![Keyboard and Trackpad](/img/chromebook_plus/c.jpg)
相比起来，键盘和触摸板就有点平平无奇。我不是说它不好，它远远比我用过的最差的要好，只是它毫无特点，除了Chromebook默认的奇怪键位之外就没有任何能够让我记住的特点了。  
## 笔槽与接口
![Left IO](/img/chromebook_plus/left_io.jpg)
![Right IO](/img/chromebook_plus/right_io.jpg)
![Penhold](/img/chromebook_plus/penhold.jpg)
接口是这台机器的一个很有意思的地方。左右各一个全功能Type-C，左边还有耳机和TF卡，右边则是S-Pen和电源音量键。对于一台笔记本电脑来说，这种IO显然是过于稀少，但考虑到Chromebook的网络属性，那么这个问题倒也不显得那么致命了。SPen因为机身尺寸可以直接收纳进机身，这是一个很棒的设计，曾经在三星的P600等平板中昙花一现，现在也只有手机和Chromebook能够享受，而理由也很简单-太占空间了。  
## 电池
![Battery Front](/img/chromebook_plus/battery_front.jpg)
![Battery rear](/img/chromebook_plus/battery_rear.jpg)
电池实在是没啥特点，一块39Wh的电池，是典型的三星笔记本电池设计语言。由于我这台机器是二手，电池续航时间并不可靠，但是也能保证四个小时以上的高强度使用。考虑到这台机器的屏幕，这一成绩并不算差。
# 硬件
![Google OP1](/img/chromebook_plus/soc.jpg)
这台机器正如上文所言搭载了国产的RK3399高性能SoC平台。这一平台包括两个Cortex-A72核心和四个Cortex-A53核心，分别运行在1.8Ghz和1.4Ghz的频率上。GPU则是一枚Mali-T864，虽然性能不算很强但是在这台机器上运行十分流畅。这颗SoC不仅在Chromebook上发光发热，也大量用于TV盒子、开发板中，甚至Pine64利用这颗SoC做出了一台传统的笔记本电脑-Pinebook Pro，而这台电脑也是RK3399这颗SoC进入我的视野的契机：作为一个长期的自由软件用户，我切换到基于ARM架构的Linux笔记本除了Steam之外就没有任何压力，加上我还有一台完整的x86PC可以用于高性能需求操作，此时使用ARM架构带来的在续航、发热量上的优势就可以展现出来，可以做到“我全都要”。而也正是这些理由，加之与Google生态的完美融合，以及ArchLinuxARM的官方支持使我选择了这台Chromebook Plus。  
不过，如果SOC性能只是刚好够用的话，那么RAM和eMMC就不能这么说了。
![maybe emmc?](/img/chromebook_plus/maybe_emmc.jpg)
似乎是由于定位原因，Chromebook很喜欢使用eMMC作为存储器。虽然高质量的eMMC连续读写速度也能够接近固态硬盘水准，且其IOPS远超机械硬盘，但由于其使用串行总线，其使用体验仍然不佳。而且，这台机器只有32GiB的内置存储也实在是过于稀少。  
对于两三百美元的Chromebook来说可能并不算什么，但对于一台上探到传统笔记本定价区间的Chromebook来说，使用eMMC存储器显然是一个很大的败笔，这也是我一直不考虑购买Chromebook的原因。当然，也有一些Chromebook采用了基于SATA或PCIe总线的存储器，它们的使用体验就会好很多，而我之前提到的Pinebook Pro也能够通过购买转接器配件的方式安装NVMe存储器使用。而RAM方面，由于RK3399平台的限制，这台机器已经顶格配满4GB内存。虽然对于ChromeOS这样一个从init就为了低配置平台优化的操作系统并没有什么大碍，但如果要使用Android或Linux容器，那么4GB内存就真的捉襟见肘。如果说条件允许，我个人会希望能够使用上16G的内存和可更换的M.2 2280固态硬盘而非4GB+32G eMMC。  
# ChromeOS
如果说硬件还算是可圈可点，那么软件，with all due respect，只能用难以下咽来形容。  
首先，由于ChromeOS是商业操作系统，其支持周期如同Android一样被限制。一般来讲，一台ChromeOS设备获取安全更新与操作系统更新的周期是五年，也就是说这台设备的支持会停止在2023年8月份。如果只是两三百美元的Chromebook，那么换了就换了，但这个价位只给五年支持，显然是将设备安全放在Google手上，是不合理的。作为一个专业用户，我可以自己安装第三方操作系统甚至尝试backport安全补丁，但是难道ChromeOS用户人均Linux开发达人？  
由于ChromeOS本身是一个基于Chrome浏览器为核心打造的操作系统，其权限设置与应用支持对poweruser极度不友好。在常见Linux发行版中必备的包管理器无处可寻，像nano这样的编辑器也需要手动安装。至于Linux容器，基于LXC技术导入的Debian 10虽然确实足够好用，但对于ChromeOS自带输入法的支持比较差，手动配置比较麻烦，加上其他的小问题，其使用体验是远远不如原生的Debian 10的。
![Trinity](/img/chromebook_plus/chromeos+linux+android.png)
更为致命的是，似乎是由于驱动问题，在使用基于Debian容器的Visual Studio Code编辑器时极为卡顿，使用体验基本为零。而且，不知道是Google设计原因还是LXC技术本身的限制（我对虚拟化一块涉猎不深），其“硬盘容量”无法动态调整只能定死，如果后期需要调整则会比较麻烦。不过，有一说一，这套Debian容器的好处是GUI应用可以做到原生支持无需额外调整，VLC、Firefox、VSCode等各种应用都可以正常地运行-除了可能存在的性能损失。说实话，一个容器性能损失如此之大我是没想到的。  
哦对了，顺便一说，Debian容器内核版本和ChromeOS内核版本还是不一样的，觉了  
![Different Kernel Version](/img/chromebook_plus/kernel.png)
至于Android么......比较尴尬。有的应用兼容很棒，有的应用倒也不是兼容不好就是不适合这个usecase，还有的应用就是勉强能用。ChromeOS要求安装第三方apk必须进入开发者模式而非像Android一样只要在设置中启用，否则就只能使用Play Store中的应用程序，这已经是很不方便了，而由于ChromeOS中的Android仅仅是一个“兼容层”，其使用逻辑还是ChromeOS式而非Android式的，这就导致在例如漫画App的使用情景中，返回主菜单需要从屏幕边缘划入，而这又跟漫画App换页的手势冲突，加上用户的使用习惯问题，使用体验十分尴尬。  
![Reading manga via Tachiyomi](/img/chromebook_plus/comic.jpg)
总而言之，ChromeOS不同于任何你可能熟悉的Linux发行版，但如果你的需求可以用浏览器和Google全家桶全部解决，那么它的体验也不算太差。  
“那就安装Arch Linux ARM啊” I hear you say，butt，问题又来了。由于这台机器采用的是ARM平台，引导第三方操作系统远远没有传统x86-64平台方便。
![fstab on this Chromebook](/img/chromebook_plus/partation.png)
由于ChromeOS的限制，其boot分区仅能使用32MiB的文件，而目前ArchLinuxARM项目官方提供的、专门为该笔记本适配的ArchLinuxARM镜像的vmlinux.kpart文件已经超出这一限制，用户可能需要自行编译内核解决；如果使用通用的ArchLinux ARM for arm64，可以启动但一直黑屏。由于时间关系，我也无法去仔细研究，所以传统Linux发行版的过程就pass掉。
# 性能
由于ChromeOS独特的性质，在性能测试环节我们就跑一些简单的项目搞定。测试中所有软件都是目前的最新版本  
首先是Android下使用安兔兔跑分。不知为何，GPU跑分无法进行，可能是兼容性问题，结果就是虽然在验机环节能够检测出GPU但总分达到了十分尴尬的11万分。
![Antutu Benchmark](/img/chromebook_plus/antutu.png)
![Antutu Check](/img/chromebook_plus/antutu_check.png)
这是什么概念呢？搭载骁龙650处理器的索尼Xperia X Compact水平。作为Xperia XC的前机主，如果兼容性问题解决这个性能应对大多数应用都是没有问题的。
接下来是Linux容器下使用UnixBench测试，成果如下
![UnixBench in Container](/img/chromebook_plus/unixbench.png)
测试结果文件放在[这里](/bench/cbp/unixbench.html)。成绩不算差但也不惊艳。
# 总结
这台机器究竟是软件拖慢硬件，还是硬件拖垮软件？我不知道，我也不好说。一来，RK3399即使能够冠以“高性能”的名号，也并非无人能敌。28nm制程带来的发热、老旧架构在性能和能耗比上都没有优势；二来，32G的eMMC闪存即使靠ChromeOS的神油优化做到一般场景下感知不强，但一旦开始高负载就能够清楚地感知到。三来，ChromeOS本身在使用上也并非完美无瑕。作为一个更偏好于传统Linux发行版的用户，我个人确实并不喜欢ChromeOS做的一些简化。对于我来说，使用Arch Linux+Chrome的成本并不比使用Chromebook高很多，但其在灵活性和自由度上肯定吊打Chromebook。即使考虑无缝耦合的Android，试问我为什么不额外购买一台Android平板来get the job done呢？但是，我们也必须看到，假设你对PC的需求仅仅是处理文档、浏览网页，并且可以流畅使用Google全家桶，那么此时ChromeOS的体验显然是极其舒适的，加上Chromebook低廉的售价，也难怪在海外能够高歌猛进。    
