---
title: 前端日常记录（一）
date: 2017-06-25 09:10:40
categories: 前端
tags: [bug记录]
---
<Excerpt in index | 首页摘要> 
前端日常记录
<!-- more -->
<The rest of contents | 余下全文>

-----

### 1.使用css3做三角
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

### 2.将某个元素存入数组
注意push函数的返回值是存入目标数组的长度，如下
```javascript
var xx=[],
	yy;
yy=xx.push(1,4,5);
console.log(yy);
//3
//返回数字一，我们的本意是获取push以后的新数组，这样是不行的
```
得这么写
```javascript
var xx=[];
xx.push(1);
console.log(xx);
//[1]
```

### 3.IE8中删除对象的属性

```javascript
// Create an object and add expando properties.  
var myObj = new Object();  
myObj.name = "Fred";  
myObj.count = 42;  

// Delete the properties from the object.  
delete myObj.name;  
delete myObj["count"];  

// Print the results.  
document.write ("name: " + myObj.name);  
document.write ("<br />");  
document.write ("count: " + myObj.count);  
// Output:  
//  name: undefined  
//  count: undefined  
```

