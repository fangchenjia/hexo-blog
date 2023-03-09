---
title: hexo怎么写博客
toc: true
mathjax: false
summary: 第一次写博客，markdown也都是刚刚临时学的，便充当笔记
categories: Markdown
keywords: Markdown Hexo 博客
tags:
  - Hexo
  - Markdown
abbrlink: a6b3d09b
date: 2020-09-16 09:25:00
---

### 首先新建文章

```bash
$ hexo new "文章标题"
```

<!--more-->

在网站根目录的 source/\_posts 目录下存放着博客文档，以.md 文档格式存储。

### 关于 Markdown 的基本语法

#### 1.标题

一个#号加空格表示一级标题，俩个#号加空格表示二级标题...依此类推，最多 6 级，如：

```
## 标题
### 标题
```

![示例](https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/blogpostimg/%24RGTQS1O.png "e")

---

#### 2.超链接 引用

```
[百度](http://www.baidu.com)
```

[百度](http://www.baidu.com)

```
>这是一条引用
```

> 这是一条引用

---

#### 3.代码块

分别用 3 个连续的符号\`\`\`包裹代码，开头三个\`\`\`末尾可写入指定的编程语言，如\`\`\`c

```
` ` `c
include <stdio.h>
int main(void)
{
printf("Hello world\n");
}
` ` `
```

```c
include <stdio.h>
int main(void)
{
printf("Hello world\n");
}
```

还有行内式,如

```
js控制台输出代码`console.log()`
```

js 控制台输出代码`console.log()`

#### 4.转义

Markdown 中的转义字符为\，如

```
\\ \* \`
```

\\ \* \`

---

#### 5.缩进、换行、空行、对齐方式

###### 首行缩进

```
【1】 &emsp;或&#8195; //全角
【2】 &ensp;或&#8194; //半角
【3】 &nbsp;或&#160;  //半角之半角
```

【1】&emsp;全角
【2】&ensp;半角
【3】&nbsp;半角之半角

###### 换行

由于 markdown 编辑器的不同,可能在一行字后面，直接换行回车，也能实现换行，但是在 Visual Studio Code 上，想要换行必须得在一行字后面空两个格子才行。

###### 空行

在编辑的时候有多少个空行(只要这一行只有回车或者 space 没有其他的字符就算空行)，在渲染之后，只隔着一行。
也可以直接使用 html 标签，即 \<br/> 。Markdown 支持直接使用 html

###### 对齐方式

```
<center>行中心对齐</center>
<p align="left">行左对齐</p>
<p align="right">行右对齐</p>
```

<center>行中心对齐</center>
<p align="left">行左对齐</p>
<p align="right">行右对齐</p>

---

#### 6.斜体、粗体、删除线、下划线

```
*斜体*或_斜体_
**粗体**
***加粗斜体***
~~删除线~~
<u>下划线</u>
```

*斜体*或*斜体* **粗体** **_加粗斜体_** ~~删除线~~
<u>下划线</u>

---

#### 7.插入图片

```
<center>  <!--开始居中对齐-->
![图片Alt](图片地址 "图片Title")
</center> <!--结束居中对齐-->
也可以直接使用html
<img src="图片地址"> </img>
```

#### 8.无序列表、有序列表

###### \* + -均表示无序列表]

```
* 无序列表项
+ 无序列表项
- 无序列表项
```

- 无序列表项

* 无序列表项

- 无序列表项

###### 有序列表则使用数字接着一个英文句点

```
1. 有序列表项
2. 有序列表项
3. 有序列表项
```

1. 有序列表项
2. 有序列表项
3. 有序列表项

---

##### 9.分隔线

你可以在一行中用三个以上的星号、减号、底线来建立一个分隔线，行内不能有其他东西。你也可以在星号或是减号中间插入空格。下面每种写法都可以建立分隔线：

```
* * *
***
*****
- - -
---------------------------------------
```

### 关于 mardown 的编辑器

&emsp;可参考文章https://blog.csdn.net/davidhzq/article/details/100815332
