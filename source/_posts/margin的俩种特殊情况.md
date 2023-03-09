---
title: margin的俩种特殊情况
categories: CSS
tags:
  - CSS
keywords: margin
abbrlink: a2c14f7
date: 2020-10-09 20:32:17
---
# margin的两种特殊现象（了解）

## marign的合并现象

> 当两个盒子**水平**布局时，左右的margin会叠加；
>
> 当两个盒子**垂直**布局时，上下的marign会合并-》合并之后取两者的最大值为两个盒子之间的距离
<!--more-->
```js
// 盒子左右排序  没毛病
 margin-left 和 margin-right 叠加

// 盒子上下排序  有问题
margin-top 和 margin-bottom 合并

// 总结 : 
两个div上下排序, 在进行设置 margin-top 和 margin-bottom 的时候,两个margin会产生一个合并的现象, 合并的值以大的为准
```

![相邻元素合并](https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/blogpostimg/www.png)

**解决方案：**   避免就好了

## margin的塌陷现象

> **嵌套** **块元素**垂直外边距的塌陷（父元素一起往下移动）
>
> 两个盒子为父子关系时候，父元素的marign和子元素的margin会合并，并且父元素会往下移动

```
如果一个大盒子中包含一个小盒子, 给小盒子设置 margin-top 大盒子会一起向下平移
```

![垂直元素合并](https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/blogpostimg/n.png)

##### ----------------------------

**解决方案：**

- 给父盒子加一个边框
- 给父盒子加 padding-top 
- 给父盒子设置属性 overflow: hidden => BFC;
- 给父盒子设置浮动
- 给父盒子设置为行内块

# 拓展

## 关于行内的padding和margin使用

什么时候设置margin? 什么时候设置padding?

```js
需要在`边框内部`留有空隙 => padding
需要在`边框外部`留有空隙 => margin
```

**块**级元素和**行内块**元素使用 margin 和 padding-》没毛病，但是：

- **行内**元素使用**margin**的left 和 right可以，top和bottom无效
- **行内**元素使用**padding**的left和right可以，top和bottom无效


