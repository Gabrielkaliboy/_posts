---
title: javascript数学函数
date: 2017-07-11 19:15:40
categories: 前端
tags: [javascript]
---
<Excerpt in index | 首页摘要> 
javascript数学函数
<!-- more -->
<The rest of contents | 余下全文>

### 1.绝对值
语法：`Math.abs()`
eg:
```
Math.abs(-9);
//返回9
```

### 2.大于等会x的最小整数（上取整）
语法：Math.ceil(x);
eg:
```
Math.ceil(1.2);
//返回2
Math.ceil(1.6);
//返回2
```

### 3.小于等于x的最大整数（下取整）
语法：Math.floor(x);
eg:
```
Math.floor(2.9);
//2
Math.floor(2.1);
//2
```

### 4.四舍五入
语法：Math.round(x);
eg:
```
Math.round(2.1);
//2
Math.round(2.9);
//3
```
### 5.π
语法：Math.PI
eg:
```
Math.PI
//3.141592653589793
```
### 可能会用到
![](https://github.com/Gabrielkaliboy/markdown/blob/master/images/images/triangle.jpg?raw=true)

### 6.正玄
语法：Math.sin(x);
注意：这里的x如果只是传入1,2,3这样的数字，他代表的可能是弧度（未验证），反正Math.sin(30)不等于0.5，需要与5合起来用。
eg:
```
Math.sin(30);
//-0.9880316240928618
Math.sin(Math.PI/6);
//0.49999999999999994
```

### 7.余弦
语法：Math.cos(x)
eg:
```
Math.cos(Math.PI/3);
//0.5
```
### 8.正切
语法：Math.tan(x);
eg:
```
Math.tan(Math.PI/4)
//0.9999999999999999
```