---
title: background属性
categories: CSS
tags:
  - CSS
keywords: css background 背景
abbrlink: '8232e008'
date: 2020-10-07 20:22:11
---
# 背景相关的属性（background）

## 背景颜色

> 设置标签的背景颜色
<!--more-->
**代码：**`background-color: red;`

## 背景图片

> 设置标签的背景为图片

**代码：**`background-image: url(图片路径);`

**注意：**

- 背景图片默认平铺

## 背景平铺

> 设置标签的背景图片是否平铺

**代码：**`background-repeat: no-repeat；`

**取值：**

- repeat：平铺 （默认值）
- no-repeat：不平铺
- repeat-x：水平平铺
- repeat-y：垂直平铺

## 背景位置

> 设置背景图片的位置

**代码：**`background-position: 水平方向的位置（x） 垂直方向的位置（y）；`

**取值：**

- 1.关键字
  - 水平方向：left、center、right
  - 垂直方向：top、center、bottom

- 2.像素：当前盒子的左上角为（0,0）原点，构建一个坐标系。第一值是X轴的位置，第二个值是Y轴的位置 交互的点就是图片左上角顶点开始显示的起始位置。
  注意：
  	1、浏览器里面的坐标系X轴水平向右  Y轴垂直向下
  	2、注意顺序

## 背景的连写

> 背景属性相关的连写形式

**代码：**`background: #fff url() no-repeat  center center;`

**注意：**

- background：背景颜色 背景图片地址 背景平铺  背景位置;（推荐使用这个顺序！）

- 省略：

```css
background: color image repeat position;
省略 :  color /  image repeat position;（相当于background-color）

省略的特殊情况
	当div（盒子）的大小和背景图片的尺寸一样的时候
	当div（盒子）大小=背景图片的大小
	可以只写  background:url(200.jpg);  相当于只写background-image
```

- 注意写省略时候有覆盖的问题（省略写法，没写就是默认值，默认值也会覆盖！）
