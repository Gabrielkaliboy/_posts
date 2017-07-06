---
title: jQuery源码分析
date: 2017-07-05 20:00:40
categories: 前端
tags: [jQuery]
---
<Excerpt in index | 首页摘要> 
jQuery源码分析
<!-- more -->
<The rest of contents | 余下全文>

-----
### 1
官网：http://jquery.com/
##### 1.1 版本选择
jQuery在2.0版本以后就不在支持IE6/7/8了，我们的版本选2.0.3。之所以选择这个，是因为他不支持IE6/7/8以后会在代码里面减少很多兼容的写法！（未压缩版）

##### 1.2简化jQuery框架
- 21-94 定义了一些变量和函数jQuery=function（）{}；

- 96-283: 给jq对象，添加一些方法和属性

- 285-347:extend:jq的继承方法。如果不明白，找点资料看看js的继承。他就是为了后续添加的方法把它挂在jQuery对象上，便于扩展

- 349-817：jQuery.extend():扩展一些工具方法。什么叫扩展工具的方法？
```javascript
$().css();
$().html();

$.trim();
$.proxy()
```
12和34是由区别的。12在面向对象中是实例的方法，34中$是函数，在函数中扩展方法是一些静态的。所以在函数下面来扩展方法的话，就是来扩展一些静态的方法。所以在jq中来给面向对象扩展静态属性和静态方法的时候，我们就把它叫做扩展工具方法。34与12的区别就是，34既可以给jQuery对象来用，有可以原生的js来用。而34只能给jQuery对象用。

可以吧静态（34）方法看做是在jQuery中最底层的东西，而实例方法（12）是上一层的更高级的东西。所以很多都是实例方法里面调用的工具方法 



- 877-2856：都是完成一个功能---->Sizzle：他的一个作用就是复杂选择器的一个实现，他是一个独立的部分。如果我们平时只是用他的选择功能，可以独立下载这个文件。在jQuery的官网左上角的第四个按钮就是。

比如：
```
$("ul li + span input.userName")
```
- 8826 将接口对外暴露
```javascript
window.jQuery = window.$ = jQuery;
``` 
##### 1.3 匿名函数自执行
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<script type="text/javascript">
		(function(){
			//好处就是变量是局部的
			var a=10;
			//函数也是局部的
			function $(){
				alert(a);
			};
		})()
		//alert(a);
		$();
		//结果就是都是报错，报未定义
	</script>
	<title>匿名函数自执行的好处</title>
</head>
<body>
	
</body>
</html>
```
jQuery把所有的代码都放在了自执行函数里面，这样他的变量就是局部的，防止和其他的变量有冲突。在jQuery里面$()和jQuery()是一样的 

##### 1.4 对外提供接口
把对外提供的方法挂在window的下面，像上面的$方法，我们挂在window的下面，就可以调用不在报错
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<script type="text/javascript">
		(function(){
			//好处就是变量是局部的
			var a=10;
			//函数也是局部的
			function $(){
				alert(a);
			};
			window.$=$;
		})()
		//alert(a);
		$();
		//此时在调用$方法，会弹出10
	</script>
	<title></title>
</head>
<body>
	
</body>
</html>
```

在当前版本中，21-94行都是定义了一些变量和函数，其中有一个函数最为重要
```javascript
jQuery=function(){};
```
这个就是我们平时用的$(),或者jQuery().jQuery中对外提供接口的位置在8860行
```javascript
window.$=window.jQuery=jQuery；
```

##### 1.5 jQuery是一个基于面向对象的
前面是一个对象，（这个里面的执行结果是对象，也可以）才能够调用后面的方法，比如jQuery中

```
$("#div1").css();
$("#div2").html();
```
这些方法的前面都是一个对象，再来看原生的
```
var arr=new Array();
arr.push();
arr.pop();
```
arr之所以后面可以跟一个方法，就是因为arr是一个数组的实例（对象）。jQuery代码里面的第63行：

```
return new jQuery.fn.init( selector, context, rootjQuery );
```