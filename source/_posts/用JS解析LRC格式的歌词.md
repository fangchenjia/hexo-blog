---
title: 用JS解析LRC格式的歌词
toc: true
comments: true
thumbnail: 'https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/cover%20(4).png'
banner: false
tags:
  - JavaScript
categories:
  - JavaScript
description:
  - 在还原网易云音乐项目的时候，遇到后台api返回LRC格式的歌词，记录一下解析的方法
abbrlink: 25b2d1a6
date: 2021-05-19 20:38:23
updated: 2021-05-19 20:38:23
---

# 用 JS 解析 LRC 格式的歌词

<!-- more -->

下面是 api 返回的数据
![](https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/blogpostimg/%E7%94%A8JS%E8%A7%A3%E6%9E%90LRC%E6%A0%BC%E5%BC%8F%E7%9A%84%E6%AD%8C%E8%AF%8D/Snipaste_2021-05-19_20-42-55.png)

## 把 LRC 歌词解析为 JS 对象

```js
createLrcObj(lrc) {
  var oLRC = {
    ti: "", //歌曲名
    ar: "", //演唱者
    al: "", //专辑名
    by: "", //歌词制作人
    offset: 0, //时间补偿值，单位毫秒，用于调整歌词整体位置
    ms: [] //歌词数组{t:时间,c:歌词}
  }
  if (lrc.length == 0)
    return;
  var lrcs = lrc.split('\n');//用回车拆分成数组
  for(var i in lrcs) {//遍历歌词数组
    lrcs[i] = lrcs[i].replace(/(^\s*)|(\s*$)/g,"")  //去除前后空格
    var t = lrcs[i].substring(lrcs[i].indexOf("[") + 1, lrcs[i].indexOf("]"));//取[]间的内容
    var s = t.split(":");//分离:前后文字
    if(isNaN(parseInt(s[0]))) { //不是数值
        for (let i in oLRC) {
            if (i != "ms" && i == s[0].toLowerCase()) {
                oLRC[i] = s[1];
            }
        }
    }else { //是数值
      var arr = lrcs[i].match(/\[(\d+:.+?)\]/g);//提取时间字段，可能有多个
      var start = 0;
      for(let k in arr){
          start += arr[k].length; //计算歌词位置
      }
      var content = lrcs[i].substring(start);//获取歌词内容
      for (let k in arr){
          let t = arr[k].substring(1, arr[k].length-1);//取[]间的内容
          let s = t.split(":");//分离:前后文字
          oLRC.ms.push({//对象{t:时间,c:歌词}加入ms数组
              t: (parseFloat(s[0])*60+parseFloat(s[1])).toFixed(3),
              c: content
          });
      }
    }
  }
  oLRC.ms.sort(function (a, b) {//按时间顺序排序
      return a.t-b.t;
  });
  /*
  for(var i in oLRC){ //查看解析结果
      console.log(i,":",oLRC[i]);
  }*/
  return oLRC
}
```

拿来就能用

转载自：https://blog.csdn.net/fenglin247/article/details/86674646
