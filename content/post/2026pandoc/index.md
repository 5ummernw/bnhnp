---
title: 如何为obsidian安装pandoc                       #文章标题
description:                     #文章简介，显示在列表卡片摘要
slug: 2026pandoc             #url的路径，例如domain/p/hello-word 
date:  2026-08-08T21:52:12+09:00   #发布日期格式，影响排序
lastmod:                         #更新日期
image:                 #封面图片，放在同文章目录下
categories:                      #分类
    - Coding
tags:                            #标签，支持多个
    - how to
weight:                       # You can add weight to some posts to override the default sorting (date descending) 权重，用于置顶或手动排序
toc : true                       #文章目录
draft : false                    #草稿
---
pandoc是obsidian的第三方插件，拓展性强的文件导出插件。

{{< details summary="0.前言">}}
重新开始用Obsidian做内容管理/优秀文章收集器。为此，想把两年前写的零碎的内容删除。删除之前做个存档。ob自己的导出选择性少，于是配置了pandoc这个插件。
{{< /details >}}

1.安装pandoc

进入pandoc[官网](https://pandoc.org/installing.html)，根据OS版本选择对应下载方式。

MacOS的下载方式，目前官网（2026/8/8）只有Intel芯片的安装包（x86_64）。M芯片的安装方法是使用homebrew:
`homebrew install pandoc`

2.配置pandoc

2.1 path

使用`which pandoc`找到pandoc所在的文件夹位置,复制。

在obsidian中从community plugin中打开pandoc的设置界面，在path中粘贴刚刚复制的内容

2.2 export folder

我选了下载文件夹

3.测试

选择任意笔记，Command+P调出仪表盘，输入Pandoc选择想要的格式。

点击确定后出现successful代表成功。

---

0.1.附1:安装了错误版本的Pandoc怎么办？

第一次安装的时候直接用了安装包，设置完之后导出一直显示“exporting”。查看pandoc的版本信息发现是intel版，记一下卸载方法。

用terminal查看pandoc的位置：`which pandoc`

用homebrew安装`brew install pandoc`

出现错误信息提醒旧版本遮挡了新安装的版本shadowed by other commands earlier in your PATH

检查新版本能否正常运行：

`/opt/homebrew/bin/pandoc --version` 显示正常版本信息

`file /opt/homebrew/bin/pandoc` 显示arm64

新版本没问题之后删除旧的版本：
`sudo rm /usr/local/bin/pandoc`

0.2.附2: homebrew是什么？

homebrew 是主要用于 macOS的“软件管家”（包管理器package manager），通过简单的命令，可以实现查找、下载、安装、升级和卸载软件。

---
see you again~
