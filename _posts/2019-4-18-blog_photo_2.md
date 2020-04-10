---
layout: post
author: Bob Guo
title: 图床记（2）
subtitle: 尝试使用Github作为图床
date: 2019-4-22
tags:  博客 图床 Github
published: true
---

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;OK，我们继续来处理问题。发生了什么问题？我的域名（bobguo.top）并没有在中国境内备案（说实话我很无法理解为什么在阿里云已经实名认证之后还算是未备案，明明域名这种东西管的相当严格），七牛云无法解析这个地址。自然我可以选择进行实名验证，但是实名验证实在过于耗时，对我来说，这个选项暂时是ダメの選択肢。看了一下原来qiubaiyang的Github页面（我的博客fork自ta的页面，如同About中所述，我已经对所有涉及个人隐私的内容进行了删除处理），他在自己博客的config页面中使用了一个来自img文件夹的图片![Alt text](/img/imgbed/github/qby's_config.png)，那么是否可以认为，我完全可以使用img文件夹作为一个图床使用，以此来上传自己的图片？很可惜，ta在博文中使用的一些图片来源于其他的网站，并非通过图床上传，故ta对博文的处理方案并非我之所好。  

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;而且，pathetically，我早在注册七牛云之前就做过类似的尝试。不知道是因为网络原因抑或是我对markdown语法并不了解，我的测试是失败的。![Alt text](/img/imgbed/github/code.png)如同各位在图片上看到的那样，我上传的一些来自我Nexus 6P的JPG文件并不能够被加载。![Alt text](/img/imgbed/github/text.png)那么，想到使用第三方图床我想是一个必然的想法吧。说实话，如果不是突然发现我的域名还没有被备案，我在前天就会直接使用七牛云作为我的图床了。  

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;于是，再次尝试使用Github就是我可能的唯一解了。打开项目文件夹![Alt text](/img/imgbed/github/repo.png)，确认图片放在/img文件夹里，然后试试通过markdown语法读取照片吧。根据这个网页：

>https://coding.net/help/doc/project/markdown.html#i-10

的内容描述，markdown里面有两种图片解决方案 - **内联**和**引用**。不过可惜的是，我根本不知道它们分别是什么意思。Google了一下，在

>https://markdown-zh.readthedocs.io/en/latest/spanelements/

里面找到了一些有关的内容。据这个网站所言，如果引用的是本地资源，可以用相对路径。比如说，我现在如果要放上我的头像，那我就要

> "![Alt text](/img/隔雨听竹2.jpg)

这样的话，我就可以在博文中插入我想要的图片。鉴于我作为一个中国死宅具有严重的网络仓鼠症，图片一般会放在本地，可以说在短期内，这个方法已经足够让我好好使用了。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;好了，图床的问题到此完结。我写了那么多博文突然发现自己相比于C或者Python更加熟悉markdown语法了。真是おめでたい(笑う).那么接下来，就是把之前的一些文章中缺失的图片都补充上去。在各位看到这篇文章的时候，补全的操作应该都已经完成了。