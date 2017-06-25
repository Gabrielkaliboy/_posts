---
title: 前端日常记录（一）
date: 2017-06-25 09:10:40
categories: 前端
tags: [less]
---
<Excerpt in index | 首页摘要> 
less学习
<!-- more -->
<The rest of contents | 余下全文>

-----

#### 使用css3做三角
使用border-color:让哪个方向有三角，就把哪个位置加上颜色，比如下面这个是向下的。下面这写法在高版本浏览器中是没有问题的，但是IE6不行，会显示黑色的方块

```css
.triangle {
  width: 0;
  height: 0;
  overflow: hidden;
  border-width: 10px;
  border-color: red transparent  transparent transparent;
  border-style: solid;
}
```

改进一下,给border-style里面对应的transparent里面写上dashed
```csss
@charset "utf-8";
.triangle {
  width: 0;
  height: 0;
  overflow: hidden;
  border-width: 10px;
  border-color: red transparent  transparent transparent;
  border-style: solid dashed dashed dashed;
}

```