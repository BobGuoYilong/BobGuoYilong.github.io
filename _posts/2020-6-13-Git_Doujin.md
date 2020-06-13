---
layout: post
author: Bob Guo
title: 用技术手段保障你的同人创作
subtitle: 利用Git维护你和你社区的同人创作作品 入门篇
date: 2020-6-13
tags: 同人 数据备份 Git
published: True #write true to publish this article.
---
# DISCLAMER
*本文章所有内容仅供抛砖引玉，在实际操作中请确认你的行为并不违反你所在国家、地区的法律。如果你有需要，本文章将以[CC-BY-SA-NC 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)协议共享。*
# DISCLAMER OVER
## 0x01 What Happened?
如果你正在看这篇文章，我相信你已经对从公元2020年2月27日开始的一系列网络冲突有所耳闻。如果你不清楚，[这里](https://zh.wikipedia.org/wiki/%E8%82%96%E6%88%98%E7%B2%89%E4%B8%9D%E4%B8%BE%E6%8A%A5%E4%BA%8B%E4%BB%B6)是事件的维基百科页面，你可以去阅读一下对目前的事态略知一二。简而言之，**饭圈内讧导致AO3被墙，中文同人创作社群遭到极大打击**，且由于内讧的饭圈至今仍未道歉，节奏爆发至今。  
在昨天（2020年6月12日），网易运营的中文内容创作平台Lofter由于涉黄被下架，在此之前该网站内部出现大量机器人发送色情图片和链接，被怀疑仍然是肖战粉丝所为。由于各个渠道传来的消息都极为悲观，作为同人创作社群的一份子，我觉得我有必要站出来提供一个我的解决方式-基于Git的分布式版本管理方案。  
使用本方案要求你拥有以下条件：
* 一台电脑，手机和平板（无论是Android还是iOS）虽然也可以适用但难度较高，我会后期专门写文章讲解。
* 基本的英语能力
* 科学上网工具（非强制）
## 0x10 Why Git?
看这篇文章的不一定有专业程序员和CS爱好者，所以在此之前，我们先要理清两个概念：Git和分布式版本管理。首先，借用一下维基百科的[解释](https://zh.wikipedia.org/wiki/%E5%88%86%E6%95%A3%E5%BC%8F%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6)，在程式设计中，分散式版本控制（英语：distributed revision control 或 distributed version control，又译为分布式版本控制），又称去中心化版本控制（decentralized version control），是一种版本控制的方式，它允许软件开发者可以共同参与一个软件开发专案，但是不必在相同的网络系统下工作。以分散式版本控制方法，作出的软件版本控制系统，称为分散式版本控制系统（distributed revision control system，缩写为DRCS，或是distributed version control system，缩写为DVCS）。简单来说，分布式版本管理可以做到人在塔在，无论是AO3还是Lofter倒了都没关系，只要还有一个人在本地存有这个文章，文章就不会丢失。而且，版本管理软件会对所有修改做记录，尤其是配合[GnuPG](https://zh.wikipedia.org/wiki/GnuPG)等密码学软件对修改用电子签名记录后，一旦涉及版权争端将会成为保护合法权益的非常有力的武器。而Git，就是众多分布式版本管理软件中的佼佼者。它由大名鼎鼎的[Linus Torvalds](https://zh.wikipedia.org/wiki/%E6%9E%97%E7%BA%B3%E6%96%AF%C2%B7%E6%89%98%E7%93%A6%E5%85%B9)开发，是目前最广泛使用的分布式版本管理软件之一。上到Linux内核和Android Open Source Project，下到大学生CS50作业，Git都可以管理。而对于大多数同人创作的图片和文字来说，利用Git来管理可谓再好不过了。而且，有很多网站可以提供免费的Git项目托管，例如[GitHub](https://github.com/)、[GitLab](https://about.gitlab.com/)和[码云](https://gitee.com/)。无论是这三家的哪一家都可以免费为你部署一个静态页面，而为了方面我们这里就选择使用GitHub，GitHub官方制作了一个在Windows和MacOS下使用的Git桌面前端，适合不喜欢在命令行里面捣鼓的人。当然，如果你对任何一家服务不爽了，你可以很快把你的项目迁移到另一家平台上。
## 0x11 How to start?
首先，在开始之前，在你的本地电脑上安装GitHub Desktop。为了方便起见，本教程使用Windows 10作为演示平台，如果你是Mac用户除了下载软件并安装的方式不同之外其他方面也没有太大的区别；Linux用户应该可以自行安装Git并部署数字签名，若不会也可以等我后面Android用教程。  
从[这个地址](https://desktop.github.com/)下载这个基于MIT协议开源的软件并安装到你电脑上。由于它挂载在GitHub服务器上，访问速度会比较慢，这里就需要用到科学上网工具。由于科学上网工具存在潜在的法律风险，在此不对这方面做过多赘述，请自行体会个中含义。下载得到的应该是一个exe文件，双击点开就会自动安装，![Alt text](/img/git/github_install.jpg)  
然后弹出软件页面。
另外一个需要安装的软件是一个文本编辑器。不，我不是说你电脑上的Word。如果你曾经是在Lofter、简书这类平台上写作过的人，你应该知道如何使用markdown。在电脑上，我们需要安装一个文本编辑器来对Markdown文件进行编辑。我这里推荐使用微软的Visual Studio Code，![Alt text](/img/git/vscode_markdown.jpg)免费开源又好用，还有跨平台，无论你是程序员还是普通用户都很适用。当然，如果你有自己的偏好那请务必继续使用，大部分现代编辑器都对Markdown有比较好的支持，完全没有必要更换。打开[Visual Studio Code](https://code.visualstudio.com/)网站![Alt text](/img/git/vscode_homepage.jpg)，点击页面上“Download For Windows”字样就可以下载安装文件，安装也十分简单。  
安装完成之后，你会看到一个界面![Alt text](/img/git/github_start.jpg)，点击[Create Free Accuont](https://github.com/join?source=GithubDesktop)，注册完帐号之后就可以登陆了。![Alt text](/img/git/github_register.jpg)注册账号的具体流程请按照说明操作，由于会涉及到验证邮件，请务必使用自己真实的邮箱。![Alt text](/img/git/github_reg_email.jpg)
## 0x100 Start a Github Pages project
现在你已经成功注册好一个GitHub账户了，下一步就是获取一个GitHub Pages页面了。  
Github上有很多人部署了个人博客，你可以Fork其中的一个repo到自己的账户上，删除他们的文件，并“据为己有”。当然，有的人可能不同意你是用他们的模板，所以在使用之前请务必确认对方已经明确在README里面提及类似字样或获取书面说明，而且在你做好的repo里也最好留下源repo的地址以示尊重。如果你找不到自己喜欢的，可以使用我的博客的模板，地址在[这里](https://github.com/PegionFish/PegionFish.github.io)。  
打开网页浏览器，输入 github.com ，回车进入，在首页选择sign in，输入你注册时登记的用户名和密码登录，然后你会看到这样一个页面。![Alt text](/img/git/github_web .jpg)这个页面就是你的个人主页，你所有的项目和动态都会在这个页面里展示出来。右上角的头像点进去可以调整你的个人设置，但我们先不处理，先在左上角Search or jump to..这里输入我的个人ID PegionFish ，搜索。你会发现提示找不到任何跟PegionFish匹配的repository。![Alt text](/img/git/github_no-repo.jpg)这里我们就需要点击旁边的Users，看到那个熟悉的头像了吗？没错，是我。![Alt text](/img/git/github_user.jpg)当你看到这篇文章的时候，会有两个PegionFish，都是我。第二个就是我这次教程中注册的账号。你可以点击Follow在GitHub上关注我，不过不点也没有问题。点开写着“鸽鱼”两个字的超链接打开我的[个人主页](https://github.com/PegionFish)![Alt text](/img/git/github_homepage.jpg),就可以看到我的博客了。在我博客页面的右上角有个写着Fork的按钮，按一下，我博客的repo就会被复制到你的账户上。接下来，我们就要对复制过来的博客进行修改，删除上一个主人的所有资料并修改成你自己的。
