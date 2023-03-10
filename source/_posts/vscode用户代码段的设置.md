---
title: vscode用户代码段的设置
toc: true
comments: true
banner: "https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/cover.png"
tags:
  - vscode
categories:
  - tool
description:
  - vscode常用的使用技巧
keywords:
  - vscode
  - 用户代码段
  - 自动
  - 填充
abbrlink: c259061d
date: 2020-11-16 20:01:46
updated: 2020-11-16 20:01:46
---

使用 vscode 开发过程中很多代码是非常常用的，每次都一个一个敲出来比较麻烦，可以通过`管理`->`用户代码片段(User Snippets)` 自定义设置快捷自定义代码段提高效率。

<!-- more -->

![](https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/blogpostimg/vs%E7%94%A8%E6%88%B7%E4%BB%A3%E7%A0%81%E6%AE%B5/vscode_1.png)
![](https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/blogpostimg/vs%E7%94%A8%E6%88%B7%E4%BB%A3%E7%A0%81%E6%AE%B5/vscode_2.png)

此处以添加 JavaScript 快捷自定义代码段为例

在搜索框输入 JavaScript

![](https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/blogpostimg/vs%E7%94%A8%E6%88%B7%E4%BB%A3%E7%A0%81%E6%AE%B5/vscode_js.png)

如果只有一行代码，例如添加`doucument.getElementById()`快捷代码块

```
"根据id获取元素": { //"xxx"引号内为描述信息
		"prefix": "getid", //"getid"此处为要添加的快捷代码
		"body": "document.getElementById('$1')" ,//$1表示第一次光标停留的位置
		"description": "根据id获取元素"
	}

```

![](https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/blogpostimg/vs%E7%94%A8%E6%88%B7%E4%BB%A3%E7%A0%81%E6%AE%B5/vscode_3.png)

![](https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/blogpostimg/vs%E7%94%A8%E6%88%B7%E4%BB%A3%E7%A0%81%E6%AE%B5/vscode_4.png)

多行代码块，例如

```
"对j的for循环": {
		"prefix": "forj",
		"body": [
			"for (var j = 0; j < $1; j++) {",
			"   $2", //$2表示光标在$1位置时按tab键后光标跳转的位置
			"}"
		],
		"description": "对j的for循环"
	}
```

注意：

注意`,`号，除了最后一个代码块，每写一个代码块都需要加`,`号
