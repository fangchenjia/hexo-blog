---
title: hexo踩坑
summary: hexo踩坑
categories: Hexo
keywords: Hexo
tags:
  - Hexo
abbrlink: 3308974b
date: 2020-09-26 10:04:15
---
hexo g 后出现错误：
```
err: YAMLException: can not read a block mapping entry; a multiline key may not be an implicit key at line
```
<!--more-->
可能原因：创建的md文件头部声明中格式问题

比如：
    
    ---
    title: hexo踩坑
    date: 2020-09-26 10:04:15
    summary: hexo踩坑
    categories: hexo
    keywords:hexo ---->冒号后面未加空格
    tags:
      -hexo ----> "-"后面未加空格
    ---
    


