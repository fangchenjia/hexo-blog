---
title: vertical-align
categories: CSS
tags:
  - CSS
keywords: vertical-align
abbrlink: e72b8332
date: 2020-10-12 09:24:32
---
# vertical-align（垂直对齐方式）

> 让图片（行内块元素）和文字对齐，需要优先给行内块元素设置垂直对齐方式
<!--more-->
**问题：** 图片和文字在一行中显示的问题

```
如果文本与图片在同一行中显示，其实默认的效果是图片的底部和文字基线对齐的，此时就可能会影响页面的布局。
此时可以通过：
vertical-align: 可以设置文本与行内块（图片）的垂直对齐方式
```

**取值：**

- baseline：基线对齐
- top：顶部对齐
- middle：中线对齐
- bottom：底部对齐

**使用行内块元素可能会出现的bug：**

- 场景1 :  文本框（text）和表单按钮（button）无法对齐问题；
- 场景2 :  input 和 img无法对齐的问题；
- 场景3 : div里放一个文本框 ，此时文本框无法靠顶；
- 场景4：div有img标签撑开，此时img标签下方有间隙（给img标签设置vertical-align即可）；
- 场景5 : 使用line-height让img标签垂直居中，需要给img标签单独设置vertical-align：middle