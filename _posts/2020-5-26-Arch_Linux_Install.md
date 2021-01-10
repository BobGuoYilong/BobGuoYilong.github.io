---
layout: post
author: Bob Guo
title:  ようこそ　我が胎内え
subtitle: 如何快速安装Arch Linux
date: 2020-5-26
tags: Arch Linux
published: true #write true to publish this article.
---
Arch好处都有啥？谁说对了就给他！aur安装开源项目顶呱呱，滚动更新爽过维他柠檬茶；所有包都自己选，还有ArchLinuxCN帮大忙。但是，安装arch实在是一个痛苦不堪的事情。即使你已经熟悉如何用GNU/Linux正常的工作生活，第一次安装Arch Linux仍然会耗费你十万甚至九万个CPU Cycle去排障和Debug。我这篇文章也只是希望让更多第一次安装Arch但对Linux已经有一定了解了的小白可以更快地进入这个世界，所以不会对一些特别细致的需求作出介绍。如果你是纯萌新想把自己的第一次交给Arch Linux请参阅[Arch linux官方安装指南](https://wiki.archlinux.org/index.php/Installation_guide)或[给 GNU/Linux 萌新的 Arch Linux 安装指南](https://blog.yoitsu.moe/arch-linux/installing_arch_linux_for_complete_newbies.html)若有任何疏漏或问题请不吝赐教，谢谢ナス。
# 0x01 前置需求
基本技能清单：

* Linux日常使用。我个人觉得Arch Linux不大适合纯小白，更适合半白不白及以上的那种，比如当年的我。这种人的特点就是稍微懂得一点怎么用Linux学习生活，也对往更深入的学习感兴趣。由于安装Arch Linux的时候需要对整个系统进行手动配置，对于小白了解Linux基本文件结构还是很有帮助的。当然，第一次就交给Arch而不是Ubuntu等发行版也是可以的，我只是不推荐。

* 魔法。这点不多说，懂得自然懂。Arch Linux官方repo和Arch Linux CN都有国内镜像，需要魔法的地方主要还是像Google Chrome或者Andorid Studio等Google软件或一些aur包会需要，所以如果真的没有也不要紧，这个问题不是很致命。
>It's LeviOsa, not LevioSA. --Hermione Granger

* 基础的英语阅读能力和排障能力。由于Arch Linux的安装全流程都在Shell里进行，加之Arch Linux充实的文档，你起码需要有一点最基础的英语阅读能力才能方便地从Wiki获取资料。最起码最起码如果你的GUI崩了屏幕上显示wipe data你不会点进去丢失所有个人文件然后还要怪开发者不给你翻译。

基本配置清单：  
根据Arch Linux Wiki[页面](https://wiki.archlinux.org/index.php/Installation_guide)的描述，Arch Linux可以在任何至少有530MiB内存和2GiB硬盘的x86_64架构机器上运行。安装过程需要从网络上下载大量的文件，所以你也需要有一个稳定的网络链接。
# 0x10 安装前准备
Arch Linux跟任何一个Linux发行版一样，需要制作启动盘。你可以从[官方链接](https://www.archlinux.org/download/)找到BT种子、Docker镜像、iso文件等多种方式。具体的烧盘方式只需要使用[rufus](https://rufus.ie/)或者[etcher](https://www.balena.io/etcher/)等工具将iso文件烧录进U盘即可。如果你是一个脱盲了的Linux User，这对你来讲应该没有任何难度。唯一一个要注意的点就是一定要用你主板支持的模式烧录U盘。除非你的电脑实在是过于古老，否则你的机器都应该支持UEFI。最早的针对普通用户的支持EFI启动的机器是Apple于2006年推出的Intel iMac系列，而从2012年Windows 8发售之后所有的新品主板都必须要支持UEFI才能通过微软认证。
# 0x11 准备安装
制作好启动盘，从USB启动并进入ArchLinux Shell界面之后，就可以开始准备安装了。  
Arch Linux，如同其他任何一个Linux发行版，都要经历配置网络时区、分区、安装软件包、安装Bootloader、个人设置等步骤。如果是那些你使用过的Linux发行版它们可能有一个图形界面来处理这些事情，但现在我们有的只有一个黑框框，全程必须使用键盘来处理。熟练使用CLI是linux小白成长为大佬的第一步：GUI很好用，我日用KDE和Android，但是很多时候，当GUI崩了，CLI才是那个你可以指望的救命稻草。诚然，装完Arch Linux之后你仍然可以跟普通的Linux一样把命令行抛诸脑后，但既然都来到Linux的世界了，为什么不give it a shot试一试呢？
# 0x100 安装前的部署与配置
由于Arch Linux的安装环境是完整的Arch Linux LiveCD，所以以下这些内容的顺序完全可以按照自己的意志决定，想先干啥就干啥。顺便提醒一句，由于我的截图是在我本人的实体机上运行的，所以会有桌面背景、窗体和中文，你在安装的时候只有英文界面。LiveCD是以root运行的，请务必小心每一步操作。如果出现意外被迫重启，除了分区之外所有的修改都会丢失。
>你们有了，我们曾经梦寐以求的权利：选择的权利 --何冰

* 时间同步

HTTPS和GnuPG这些技术都需要确保时间同步来保证加密有效，所以在安装之前我们需要手动同步时间。只要输入
>timedatectl set-ntp true

即可。

* 配置网络  

由于没有GUI，几乎所有网络配置都得手动完成。如果你的设备有RJ45网线接口请务必优先使用有线网络链接。它最大的优势就是一般不需要手动调试开箱即用，而且相较于WiFi，它更加稳定。如果你的设备并没有RJ45，你又没有dongle或不想接线，那么使用WiFi需要输入
> wifi-menu

你就会看到WiFi的列表。
![Alt Text](/img/archlinux/wifi-menu.png)  
选择一个网络，就会看到这个画面，要求你给网络的配置文件命名。这里有人可能会很仔细的写，但有一说一大可不必。在安装完成之后我们会使用另外一套网络管理系统，而且在这个LiveCD里的所有配置文件都是重启就丢失的。  
![Alt Text](/img/archlinux/wifi-menu-config.png)  
命名好配置就要输入密码。
![Alt Text](/img/archlinux/wifi-menu-password.png)  密码输入完成按回车就会回到一开始的界面，此时输入
> ping bing.com

确认已经连上网络了就可以继续。
![Alt Text](/img/archlinux/ping_bing.png)  
* 分区  

对于任何类UNIX操作系统来说，分区都是至关重要的。分区的多少和大小由你的磁盘决定，你也同样可以将多个硬盘都纳入分区表
> 你们都是我的翅膀 --早已女阿尔特

如果你在安装Arch linux之前就已经在使用Linux操作系统，那么你就不需要重新分区，只要把这些分区挂载到/mnt下即可继续;但如果你之前使用的是Windows或macOS，那你就需要重新分区了。请注意，在分区前请务必保存所有重要数据。  
你可以在WindowsPE镜像下或在Linux下进行分区，也可以将现有的分区直接格式化成对应格式。在这里我就选择用cgdisk/cfdisk来对磁盘分区。如果你使用的是UEFI，请选择前者；如果你使用的是Legacy或BIOS，请选择后者。两者的UI设计风格十分相像，而且使用起来也一样反直觉。![Alt Text](/img/archlinux/cgdisk&cfdisk.png)   
由于这份教程以UEFI为基础，cfdisk用户需要自行搜索资料。  
首先需要删除现有的所有分区。只要用方向键选中分区并找到Delete按下回车即可。  
![Alt Text](/img/archlinux/delete_partition.png)  
删除完成后，选择new新建分区。新建分区会跳出来三个选项，第一个选择起始扇区，只要回车就好；第二个选择尺寸大小，由于我们建立的是EFI分区只要留200m就可以，输入200M回车；第三个选择分区种类。这里使用16进制字节，8300代表Linux分区，而我们需要的是EFI分区，所以输入ef00。回车之后，我们就创建了一个EFI分区。  
![Alt Text](/img/archlinux/make_efi.png)  
第二步，我们要创建一个/分区。如果你对特殊环境有需求需要独立每个分区那么也是在这一步完成。跟建立EFI分区一样，起始扇区直接回车，尺寸大小按需选购，分区种类8300,回车  
![Alt Text](/img/archlinux/make_root.png)  
分区创造完毕，选择write将分区表写入磁盘。
![Alt Text](/img/archlinux/simpest_partition_table.png)  
如果你的磁盘上还有重要数据没有备份，在这一步按Ctrl+C退出，快点备份，因为按下回车之后你就回天乏力了。同样的， 如果你需要多个磁盘带来双倍的快乐，你就需要对多个磁盘进行分区并写入分区表。  
分完区之后就要进行格式化。一般只需要使用mkfs.vfat和mkfs.ext4就可以格式化分区。
假设我现在有这么一个情况：一张机械硬盘一张NVMe固态硬盘，/boot跟/hdd放在机械硬盘上，/和/home放在固态硬盘上，那么我分完区之后要做的就是
> mkfs.vfat /dev/sda1 && mkfs.ext4 /dev/sda2 && mkfs.ext4 /dev/nvme0n1p1 && mkfs.ext4 /dev/nvme0n1p2

这一段指令会让系统自动格式化所有需要的分区，后三者由于需要安装linux就会使用ext4。  
格式化完成之后就要进行挂载。还是上面那个例子，如果你曾经使用过linux你就会马上意识到/hdd不是一个Linux标准的文件格式。所以，在挂载完/之后我们需要新建几个文件夹以满足我们独特的需求。
> mount /dev/nvme0n1p1 /mnt # 挂载NVMe硬盘上第一个分区作为根目录  
mkdir /mnt/boot  
mkdir /mnt/hdd  
mkdir /mnt/home

有人会问，既然/boot是Linux标准的文件格式，那么为什么我们还要重新创建一个/boot呢？还记得我们之前格式化的那个EFI分区吗？没错，它就是要挂载到/boot上的。如果我们需要把特定的分区挂载成特定的文件夹就需要提前建立并挂载。  
格式化完了，文件夹也建立好了，我们现在要做的就是挂载上去。
> mount /dev/nvme0n1p2 /mnt/home # 挂载NVMe硬盘上第二个分区作为/home  
mount /dev/sda1 /mnt/boot  
mount /dev/sda2 /mnt/hdd

到此，分区的部分就基本完成了。

* 选择镜像  

镜像的速度决定了你安装的速度有多快。Arch Linux的镜像遍布全球，而默认的/etc/pacman.d/mirrorlist是随机分布的，所以默认状态下速度极慢，我们就需要手动调整镜像文件来选择最快的镜像。这里我们就要借助一个软件包，它的名字叫做[reflector](https://wiki.archlinux.org/index.php/Reflector)。在使用之前，你需要
> pacman -Sy

更新软件包数据库。更新完成之后，输入
> pacman -S reflector

即可安装。安装完成之后，先备份现有的镜像列表，然后开始操作。
> cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.bak # 备份现有镜像列表
reflector --verbose -l 200 -p http --sort rate --save /etc/pacman.d/mirrorlist # 将最快的200个镜像罗列出来代替mirrorlist

至此，你已经成功地将镜像调整到最优。
# 0x101 安装
在配置完成之后，安装Arch Linux只需要一行命令：
> pacstrap /mnt base base-devel linux

这句命令中，pacstrap是arch-install-scripts的组成部分，它可以在某个文件夹里安装Arch Linux的软件包；/mnt是我们安装Arch Linux的磁盘分区挂载的文件夹；linux代表linux内核（你也可以选择安装其他版本的内核，比如linux-lts、linu-hardened和linux-zen），而base元包包括所有Arch Linux的核心软件包；除此之外建议一次性安装的有：base-devel包括主要的开发工具包（比如GCC这类）和一个文本编辑器，我们在之后的旅途中会常用到它。如果你习惯了VIM或emacs直接安装即可，但如果你并未习惯这些old school编辑器，只要使用[GNU Nano](https://www.nano-editor.org/)就可以获得大部分GUI编辑器般的手感。  
按下回车之后，系统就会自动安装所有东西。我们只需要泡杯茶等待即可。

# 0x110 安装后配置
在安装好之后，是不是迫不及待想要跳进这个rabbit hole了？别急别急，先等等，还有最后一件事情要搞定，那就是建立分区表。
输入
> genfstab -U /mnt >> /mnt/etc/fstab

然后，输入
> arch-chroot /mnt

就可以进入你刚刚亲手装好的Arch Linux系统环境了。而同样的，接下来这些操作也可以自由选择顺序。
>更年轻的Linux安装，容得下更多元的流程、配置和软件包。 --我

* 本地化（底层）

为了让你的Arch Linux如你所愿地正常的工作，我们需要对一些东西进行设置。  
首先，是设置时区和时间。中国大陆的时区一般是Asia/Shanghai，但如果你在新疆等地你可能需要使用Asia/Urumqi等不同的设置。
> ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime  
hwclock --systohc --utc

如果你同时在使用Windows双系统，请在Windows的命令行里输入这一段指令：
> reg add "HKEY_LOCAL_MACHINESystemCurrentControlSetControlTimeZoneInformation" /v RealTimeIsUniversal /d 1 /t REG_DWORD /f

否则Windows下的时间会很奇怪。  
接下来是地域设置。Arch Linux下的地域设置存在/etc/locale.gen里，用nano打开这个文件，删掉你需要的地域前面的#，保存推出然后
> locale-gen

就可以了。

* 本地化（表层）

这里你需要设置系统默认使用的语言。虽然你可以使用中文，但这回导致tty乱码，所以这里还是建议用英文，之后进入桌面了再改回中文就很好。
> echo LANG=en_US.UTF-8 > /etc/locale.conf

然后，设置一个你喜欢的主机名。在这里，我用“Arch”作为主机名，你可以自己修改。
> echo arch > /etc/hostname

修改完主机名还需要对[hosts](https://en.wikipedia.org/wiki/Hosts_(file))文件进行修改。
>127.0.0.1	localhost  
::1		localhost  
127.0.1.1	arch.localdomain	arch

还是老样子，这里的arch你得替换成你自己设置的主机名。

* 安装桌面环境

用了那么久的命令行，是不是很怀念桌面环境？接下来就是安装桌面环境和中文字体的时候了。除了xorg之外的东西都可以自己选，我这里选择安装KDE桌面，配合Firefox、VLC和Telegram，还有Fcitx-googlepinyin来输入中文。
> pacman -S xorg plasma kde-applications-meta sddm firefox telegram-desktop vlc fcitx fcitx-googlepinyin networkmanager noto-fonts noto-fonts-cjk noto-fonts-emoji adobe-source-han-sans-otc-fonts wqy-microhei wqy-zenhei

具体有哪些可以装的桌面环境可以在[这里](https://wiki.archlinux.org/index.php/Comparison_of_desktop_environments)找到。字体可以在[这里](https://wiki.archlinux.org/index.php/Fonts)找到。如果有什么想要安装的应用也可以在ArchLinux Wiki上搜索解决方案。

* 设置Bootloader

安装并设置bootloader就可以让你的机器正常的启动而不是每次都要用Arch Linux LiveCD引导，挂载上述那些分区，然后arch-chroot过去。我们这里选择用GRUB，你也可以根据自己的喜好选择其他的bootloader。
> pacman -S efibootmgr dosfstools grub os-prober

这些软件包可以安装并配置grub。  
输入这个命令以安装grub：
> grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=grub --recheck

其中，bootloader-id可以自行修改，target代表安装的架构（x86_64)，efi-directory代表安装GRUB的地址。安装完成之后，你需要自动生成一个GRUB配置文件。
> grub-mkconfig -o /boot/grub/grub.cfg

这样就基本搞定GRUB的安装和配置了。

* 设置用户权限

用户权限主要有三个部分，root密码、sudo和你的个人账户。root密码是你系统最高权限的密码，一定要保管好不能随便告诉别人，设置只需要
> passwd

即可；而你的个人账户才是每天都会使用的那个。建立自己的账户需要
>useradd -m -G wheel bob

bob可以替换成你想要的用户名，然后再
> passwd bob

创建个人密码即可。  
sudo允许你在不切换成root的前提下运行需要root才能运行的命令，在日常使用中是使用率极高的一个命令。输入
> pacman -S sudo

确认sudo是否安装，如果没有安装就把它安装上，然后输入
>visudo

开始编辑sudo。默认它使用的是vi，所以如果你没有安装vi的话会报错，这时要么安装vi要么在前面加上
> EDITOR=nano

来调用其他编辑器处理。如果你胆子够大，也可以直接
> nano /etc/sudoers

不过我个人不推荐就是了。按你胃，现在你已经在编辑sudoers的环境了，找到这一段
> ##Uncomment to allow members of group wheel to execute any command    

然后删掉下面的那个#，保存退出就大功告成了。如果你没有设置只是输入sudo，那么系统会提示你并不在sudoers里面，你的操作已经被记录，这样你就无法在不是root的前提下使用这些指令。


# 0x111 结语
想重启吗？还没有呢。最后一个任务，输入这几段命令：
> systemctl enable sddm # 这里根据你选用的桌面的不同而不同  
systemctl enable NetworkManager # 注意大小写

回车，退出，重启。
输入密码，登录，开机，欢迎来到Arch Linux的世界。记得多看看wiki，实在有不懂的可以去论坛问问题，还有ArchLinuxCN的Telegram群组可以解惑。Arch Linux跟普通的Linux发行版没有任何本质区别，只不过更加自由（当然肯定还是没有gentoo或者LFS那种自由度的）。每天记得都要来sudo pacman -Syu哟