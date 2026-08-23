---
title:  Kindle Paperwhite6 安装微信阅读                    #文章标题
description:                     #文章简介，显示在列表卡片摘要
slug: 202608koreader             #url的路径，例如domain/p/hello-word 
date:  2026-08-23T19:58:03+09:00   #发布日期格式，影响排序
lastmod:                         #更新日期
#image: cover.jpg                 #封面图片，放在同文章目录下
categories:                      #分类
    - 日常
tags:                            #标签，支持多个
    - HowTO
#weight: 1                        # You can add weight to some posts to override the default sorting (date descending) 权重，用于置顶或手动排序
toc : true                       #文章目录
draft : false                    #草稿
---
{{< details summary="碎碎念">}}
最近用微信读书app看书感觉很方便，不需要去网站下载直接搜索书名就可以看。为了更大的屏幕和护眼，更想用电子书阅读器来看。本来打算买国产的电子书阅读器，看了大家的对比，再加上不信任国产厂商的质量把控，还是决定用我手里的kindle。于是搜了一些攻略把手头最新固件版本的kindle pw6进行了越狱。

升级之前在某书搜相关的内容，看大家的评论出现不少错误，以为会很麻烦。实际自己动手大概一小时搞定。
{{< /details >}}

网上的攻略写的非常详细，我在下面贴一下我的越狱流程和参考教程。

0.准备工作：

・一台电脑，我用的是MacBook。Kindle连接macOS需要使用[USB File Manage](https://www.amazon.com/sendtokindle/mac)。

・确认kindle的版本。我的版本是Kindle pw6，官方的名字是Kindle Paperwhite 12generation。

1.进行越狱

参考的是[书伴网的教程](https://bookfere.com/post/1193.html)，非常详细，感谢书伴。

2.安装插件，koreader。

最新版本的是自动安装了包插件可以不用额外下载。但我最开始没理解什么意思，参考了[插件下载的教程](https://bookfere.com/post/311.html)，重新下载了包管理插件。装好包管理插件就可以下载安装koreader了。

2-1安装koreader插件：微信读书

微信读书是在koreader上运行的，所以要先安装好koreader之后再安装微信读书。使用了finlater大佬的开源项目，有[中文版的安装教程](https://github.com/finlater/weread.koplugin)。

2-2安装koreader插件：SimpleUI

原装版的koreader操作性上并不算优秀，在微信阅读的教程里发现有这个[插件](https://github.com/doctorhetfield-cmd/simpleui.koplugin)。在installation部分有详细的安装方法。注意下载完code之后文件名字是simpleui.koplugin-main，需要改成simpleui.koplugin，这样拷贝到kindle根目录中才能显示。

---
Huge thanks to all the devs!

and see you again
