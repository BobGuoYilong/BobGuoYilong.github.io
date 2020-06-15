---
layout: post
author: Bob Guo
title: 用技术手段保障你的同人创作
subtitle: 利用Git维护你和你社区的同人创作作品 魔改篇
date: 2020-6-13
tags: 同人 数据备份 Git
published: True #write true to publish this article.
---
# DISCLAMER
*本文章所有内容仅供抛砖引玉，在实际操作中请确认你的行为并不违反你所在国家、地区的法律。如果你有需要，本文章将以[CC-BY-SA-NC 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)协议共享。*
# DISCLAMER OVER
## 0x01 What Happened?
[上一篇文章](/_posts/2020-6-13-Git_Doujin.md)里，你已经成功地注册了一个GitHub账户，从我的Github账户上复制了一个GitHub Pages的repo过来，在这篇文章里我会手把手指导你怎么把repo改成你自己的并安排上Github Pages。
## 0x10 Download to your machine
第一步，我们需要把repo下载到电脑上。由于GitHub的网络原因，下载大量文档速度极为缓慢。我在子账号上的版本将会是一个最小系统的repo，这样会大幅简短下载时间；你也可以修改git的配置文件（Windows系统下在C:/Users/你的账户/.gitconfig），配置所有Git流量经过代理。
![Alt text](/img/git/gitconfig.jpg)
在文档的末尾加上这么一段：
> [http]  
 Proxy = 代理地址:代理端口

![Alt text](/img/git/github_proxy.jpg)
然后，保存，并在任务管理器里关闭所有Git进程即可。  
打开GitHub Pages，选择“Clone a repository from the internet”，在弹出的窗口里选中你的repo并选择地点，点击clone。![Alt text](/img/git/github_clone.jpg)稍等片刻，你就会在指定的位置发现PegionFish.github.io这个文件夹。 
![Alt text](/img/git/github_repo_complete.jpg) 
## 0x11 Delete my content
在GitHub Desktop中点击Show in Explorer，用Windows文件管理器打开这个文件夹。![Alt text](/img/git/explorer.jpg)这个文件夹里包含了所有GitHub Pages的页面文档。_posts文件夹是你所有博文的位置，img是用来存放图片的地方，其他东西你都可以丢在那里按兵不动。删除_posts文件夹里面的所有东西，并把img文件夹里所有的子文件夹和我的头像全部删除，接下来就可以开始修改配置了。请注意，虽然这系列文章以CC-BY-SA-NC4.0协议共享，并不代表我的博客中的内容也按照此协议共享。如果你在未经我授权的前提下使用了我的博文和图片，我保留使用法律手段的权利。
## 0x100 Add your own content
回到GitHub Desktop，你会发现所有被删除的东西都在Changes一栏里做了记录，这是因为Git会记录你每一个动作的历史。![Alt text](/img/git/github_commit.jpg)既然我们需要删除所有我的遗迹，那就随便写点理由，点击Commit to Master，然后点击Push Origin，将它推送到GitHub的服务器上。![Alt text](/img/git/github_push.jpg)我的图片里有You don't have write access to PegionFish.github.io，这是因为我使用的文档是直接从我的开发工作站上复制过去的。由于手动修改Git文件并未被系统自动刷新，如果你是从你自己的账户上下载下来的就不会有这个问题。  
为了修改配置文件，你需要在GitHub Desktop中点击Open in Visual Studio Code，让Visual Studio Code打开文件夹。![Alt text](/img/git/vscode_default.jpg)这个英语界面并不足够user friendly，所以我们点击左侧列第五个图标，在打开的搜索框中输出Chinese按下回车，并安装第一个官方简体中文语言包。![Alt text](/img/git/vscode_language.jpg) ![Alt text](/img/git/vscode_language_2.jpg)安装后系统会提示你自动重启Visual Studio Code以应用中文语言包，点击重启，就可以享受中文界面了。![Alt text](/img/git/vscode_language_3.jpg)  
我们首先打开_config.yml这个文件是Jekyll的配置文件，它控制了很多我们在博客网页上看到的元素。就如同这张图片展示的一样，很多元素直接由这份文档控制。所以，你需要把它改造成你想要的样子。![Alt text](/img/git/blog_config.jpg)由于这个版本只是简单做一下给个示范，所以没有怎么精细调整。按下Ctrl+S保存文件，接下来就是about.html。它类似于你的用户页，还记得之前_config.yml的sidebar吗？它就是这个的拓展版。修改，保存，然后在GitHub Desktop里上传，这样就做好了你的配置工作。
## 0x101 Tweak GitHub Settings
最后一步工序就是调整repo的设置，让GitHub认识到这是一个GitHub Pages页并对它进行加工。打开GitHub网页版，点进你的项目，点开右边的Settings，先将名字改成你的GitHub ID配合.github.io，例如我这个号是pegionfish2，所以我就要把我的项目改成 pegionfish2.github.io .![Alt text](/img/git/github_rename.jpg)接下来，输入pegionfish2.github.io，你就可以看到系统确实已经把它当作一个GitHub Pages来解析了。![Alt text](/img/git/github_pages.jpg)接下来，就是导入图片和文字了。