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

### 3.css强制换行和超出隐藏实现
一、强制换行
1 word-break: break-all; 只对英文起作用，以字母作为换行依据。

2 word-wrap: break-word; 只对英文起作用，以单词作为换行依据。

3 white-space: pre-wrap; 只对中文起作用，强制换行。


word-break:break-all 和 word-wrap:break-word 都是能使其容器如DIV的内容自动换行，它们的区别在于：

1、word-break:break-all 
假设div宽度为450px，它的内容就会到450px自动换行，如果该行末端有个很长的英文单词，它会把单词截断，一部分保持在行尾，另一部分换到下一行。

2、word-wrap:break-word 
例子与上面一样，但区别就是它会把整个单词看成一个整体，如果该行末端宽度不够显示整个单词，它会自动把整个单词放到下一行，而不会把单词截断掉。

二、禁止换行 

1 white-space:nowrap; overflow:hidden; text-overflow:ellipsis; 
white-space:nowrap; 是禁止换行。
overflow:hidden; 是让多出的内容隐藏起来，否则多出的内容会撑破容器。
text-overflow:ellipsis; 让多出的内容以省略号...来表达。但是这个属性主要用于IE等浏览器，Opera浏览器用-o-text-overflow:ellipsis; 而Firefox浏览器没有这个功能，多出的内容只能隐藏起来。
