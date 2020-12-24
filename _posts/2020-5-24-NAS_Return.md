---
layout: post
author: Bob Guo
title: 用Precision做软路由是什么体验（1）
subtitle: 本地配置OpenWRT编译环境
date: 2020-5-24
tags: 软路由 OpenWRT
published: true #write true to publish this article.
---
兄弟萌，👴回来了。  
之前在[这篇还没有写完的文章](2020-4-14-NAS_Ending.md)里我其实已经结束了尝试。由于网上能找到的教程资料对于我的环境来说实用意义不大，而我最后的底牌—本地编译由于G1840的羸弱性能也无法实现。不过，还记得我的[Precision T1700 SFF](2020-4-18-Precision_T1700_1.md)工作站吗？它的尺寸真的是小巧玲珑，配合低压Xeon做Headless服务器体验会很棒。由于我并不需要超大容量的本地存储空间，我仍然沿用原来软路由上的128G固态硬盘；而内存也改为两条4GB DDR3 1600内存组成1DPC双通道，剩下的16G内存就留作他用。如果未来出现编译AOSP或渲染视频等需求还可以再插上去组成24GB双通道。我的那张HD8570也仍然放在那里，虽然它存在那里的唯一理由就是我还没有彻底配置好Headless而我使用的Xeon没有核心显卡无法正常工作。如果未来存在对CUDA计算有要求的场景，我可能会买一张Quadro丢进去。  
# 0x01 应用环境
网卡仍然是i340，四口千兆，IBM原装，老当益壮的经典网卡。买了小尺寸挡板之后跟我的机箱很适配，而且也可以正常识别。本来我打算装一张无线网卡并通过SSH连接，但由于暂时无法成功我就先把它换成显卡，在GUI环境下工作。这张网卡的四个接口全部会被用作连接外部设备，而路由本体与网际网路的交互将会由机器板载的千兆网卡进行。  
操作系统仍然是Ubuntu 20.04 LTS版。我个人不是很喜欢在服务器上部署Arch，虽然AUR确实很好用，而且不想用Arch也属于我个人的bias，但目前我还没有达到那个境界，Ubuntu也足够好用。而且，大部分教程预设的编译环境都是Ubuntu，使用Arch Linux可能存在一些小问题，而这些问题需要多次debug才能解除。至于软路由部分，我打算使用虚拟机配合OpenWRT进行。OpenWRT是一个专门为路由器等嵌入式设备定制的Linux发行版，而相比于其他基于Linux的路由器固件，它更像传统的Linux操作系统，包括一个包管理器，可以自由地安装不同的软件。而且，它除了常见的MIPS或ARM架构之外，也支持x86架构，这也让它成为了软路由的最佳选择之一。为此，我需要在本地编译OpenWRT。
# 0x10 设置Proxychains
由于OpenWRT的源代码托管在GitHub上，而GitHub在国内的使用环境是人尽皆知的差，所以获取源码之前要做的是部署[ProxChains](https://github.com/haad/proxychains)。只要在命令前输入proxychains就可以让这条命令使用代理运行而不用调整git的代理设置，是一个更为灵活的解决方案。Proxychains在大部分发行版的官方仓库里都有，只要用你的包管理器安装Proxychains就可以了。
> sudo apt-get install proxychains

安装完proxychains，下一步就是根据你使用的代理调整*/etc/proxychains*并在末尾加入你使用的代理协议、地址与端口。对于大部分人来讲，只要加入socks5 127.0.0.1 1080即可。  
当然，你也可以本地编译一份，但这一块就在此不表。
# 0x11 获取OpenWRT源代码
OpenWRT的源代码托管在[这里](https://github.com/openwrt/openwrt)，你也可以使用KoolShare论坛的版本，但我个人还是更偏向自己动手丰衣足食，调教软路由也可以作为考研备考的一部分，而且我个人对Koolshare论坛的闭源固件并不信任，就自己本地编译咯。   
打开终端，定位到你想要的地方（比如我就放在桌面），并输入
> proxychains git clone git@github.com:openwrt/openwrt.git

如果没有什么问题，你的电脑会自动在这个地方建立一个openwrt的文件夹，并开始同步OpenWRT的源代码。具体的时长要按照你的网络状况而定，但由于文件总量比较大（毕竟这怎么说也是一个完整的Linux发行版），最好做好等待一段时间的准备。  
在下载完成后，cd到openwrt文件夹，并输入
> git checkout openwrt-19.07

这样你就会切换到OpenWRT 19.07版的分支，并可以以此为基础开始干活。
# 0x100 安装依赖
OpenWRT编译的时候会需要用到一些依赖包，这些包一般都可以在你发行版的官方仓库里找到。打开终端，输入
> sudo apt-get install gcc g++ build-essential asciidoc  binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch flex bison make autoconf texinfo unzip sharutils subversion ncurses-term zlib1g-dev ccache upx lib32gcc1 libc6-dev-i386 uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev libglib2.0-dev xmlto qemu-utils automake libtool  -y

这会自动安装所有需要的依赖。请注意，如果你的发行版不是预装Python 2的，比如Ubuntu 20.04或Arch Linux，你就需要手动安装Python 2，否则在下面的流程中你会遇到大问题的。
# 0x101 配置编译环境并获取软件包源代码
在编译OpenWRT的时候，Like all other large scale projects，你需要配置一个编译环境。OpenWRT有一个脚本可以获取编译时需要的软件包的源代码，将它一起编译到你的OpenWRT里。  
为了使用这个脚本，你需要输入以下指令：
>proxychains ./scripts/feeds update -a  
proxychains ./scripts/feeds install -a

脚本会自动完成，之后就可以开始配置并编译OpenWRT了。
# 0x110 配置并编译
输入
> make defconfig

测试你的编译环境。如果它返回了如图所示的configuration written to .config， 那你的编译环境已经布置完成，接下来就要开始配置并编译了。  
输入
> make menuconfig

进入我们熟悉的Linux内核编译配置界面。由于OpenWRT是一个跨平台的项目，我们首先要选择编译使用的平台。我这里因为是为本机编译，所以在Target System中选择x86，拉到最底就能看见了。  
第二步是进入Subtarget，并选择x86_64。64位操作系统可以更好地利用现代设备的高性能，而且也不会对编译出来的文件尺寸造成多少影响-我可是有128G固态硬盘放在这儿的（笑）  
Target和Subtarget的选择应当由你的机型而定。如果你的路由器使用了其他的硬件，这里就需要调整成其他硬件使用的配置文件。对于曾经有过Linux编译经验的人来说，除了这里其他的地方都应该知道什么意思并可以自行处理，本文也就不再过多赘述。  
当你的配置文件已经完成，现在只要保存配置文件并退出，输入
> make V=99

即可开始编译。