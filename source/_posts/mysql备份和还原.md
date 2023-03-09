---
title: mysql备份和还原
toc: true
mathjax: false
categories: mysql
keywords: mysql 基础 备份 还原
tags:
  - mysql
abbrlink: bf60a373
date: 2020-09-24 13:06:36
---

# 数据库的备份和还原

备份：

<!--more-->

```
mysqldump -u用户名 -p密码 数据库名称 > 保存的路径
```

还原：

1.  登录数据库
2.  创建数据库
3.  使用数据库
4.  执行文件: source 文件路径
