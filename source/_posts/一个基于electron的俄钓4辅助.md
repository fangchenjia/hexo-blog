---
title: 一个基于electron的俄钓4辅助
ai: true
cover: https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/%E6%B5%B7%E7%AB%BF.jpg
date: 2023-06-05 10:41:47
tags:
  - electron
  - typescript
  - express
  - 俄罗斯钓鱼4
categories:
  - 俄罗斯钓鱼4
description: 大学的时候迷上了一款游戏，叫俄罗斯钓鱼4，但是特别肝，后面就想着写一个辅助，前台用electron实现，后台使用express加ts，于是就有了这个项目
---

# 项目介绍

> 主要实现了三海竿，单杆路亚，单手竿的挂机功能，但是由于游戏的随机性，所以并不是100%的准确，但是基本上可以实现挂机，不用自己操作了
> 添加了喵提醒功能，可以在游戏中的特定时候通过微信公众提醒你，比如说上了稀有鱼

# 项目实现

> 项目主要分为两部分，前台和后台，前台使用electron实现，后台使用express加ts实现，这个项目暂时不打算开源，暂时为收费项目，有需要的可以联系我。
>
> ![image-20230605110402292](https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/image-20230605110402292.png)

## 前台
> 使用electron-vite搭建，ui框架选用的`native-ui`，对于主进程和预加载进程的代码使用nodebyte编译为了二进制文件，因为electron很容易会被解包，所以这里使用了nodebyte来加密代码，防止被解包


## 后台
> 后台数据库使用mongodb，使用mongoose来操作数据库，后台主要实现了用户的注册，登录，充值解绑，以及支付宝扫码当面付。

# 项目展示

![image-20230605110235533](https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/image-20230605110235533.png)

想体验的可以进QQ群，直接注册登录便可体验，群号：`850695539`