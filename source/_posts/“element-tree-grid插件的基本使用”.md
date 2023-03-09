---
title: “element-tree-grid插件的基本使用”
toc: true
comments: true
tags:
  - vue
categories:
  - vue
description:
  - element-tree-grid插件的基本使用
keywords:
  - vue
  - element-tree-grid
abbrlink: e29d435c
date: 2021-04-06 16:04:20
updated: 2021-04-06 16:04:20
---

# 使用方法

[码云仓库](https://gitee.com/marklov/element-tree-grid)

<!-- more -->

1、通过 npm 安装 element-tree-grid

```bash
npm install element-tree-grid --save
```

2、在 main.js 中注册 element-tree-grid

```bash
var ElTreeGrid = require('element-tree-grid');
Vue.component(ElTreeGrid.name,ElTreeGrid);
```

3、vue 文件中的 HTML 部分：

```html
<el-table
  :data="categoriesList"
  style="width: 100%">
  <el-table-tree-column
    label="分类名称"
    prop="cat_name"
    treeKey="cat_id"  //找子节点
    parentKey="cat_pid"  //找父节点
    levelKey="cat_level">  //按照等级缩进
  </el-table-tree-column>
  <el-table-column
    label="层级">
    <template slot-scope="scope">
      <span v-if="scope.row.cat_level == 0">一级</span>
      <span v-if="scope.row.cat_level == 1">二级</span>
      <span v-if="scope.row.cat_level == 2">三级</span>
    </template>
  </el-table-column>
</el-table>
```

4、vue 文件中的 js 部分：

```js
categoriesList: [
  {
   cat_id:1,
   cat_level:0,
   cat_name:"xxx",
   cat_pid:0,
   children:{
	 {
      cat_id:3,
      cat_level:1,
      cat_name:"xxx",
      cat_pid:1,
     }
   }
  }
]
```
