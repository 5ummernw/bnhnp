---
title:  {{ replace .File.ContentBaseName "-" " " | title }}                      #文章标题
description:                     #文章简介，显示在列表卡片摘要
slug: {{ .File.ContentBaseName }}             #url的路径，例如domain/p/hello-word 
date:  {{ .Date }}   #发布日期格式，影响排序
lastmod:                         #更新日期
image: cover.jpg                 #封面图片，放在同文章目录下
categories:                      #分类
    - Example Category
tags:                            #标签，支持多个
    - Example Tag
weight: 1                        # You can add weight to some posts to override the default sorting (date descending) 权重，用于置顶或手动排序
toc : true                       #文章目录
draft : false                    #草稿
---