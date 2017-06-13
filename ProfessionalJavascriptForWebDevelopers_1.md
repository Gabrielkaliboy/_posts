---
title: javascript 高级程序设计
date: 2017-06-07 20:52:40
categories: 前端
tags: [javascript]
---
<Excerpt in index | 首页摘要> 
javascript 高级程序设计
<!-- more -->
<The rest of contents | 余下全文>

-----
#### 2
##### 2.1
弹出script标签
报错
```javascript
<script type="text/javascript">
	function sayScript(){
		alert("</script>");
	};
	sayScript();
</script>
```
加入转义字符就好了
```javascript
function sayScript(){
			alert("<\/script>");
		};
		sayScript();
```
##### 2.1.1<script>标签的位置
因为javascript脚本放在header之间的话，如果页面的javascript特别多，浏览器会将javascript全部被下载，解析，执行完以后才能执行，会导致浏览器出现延迟，页面一片空白，为了避免这个问题，一般放在body后面。

##### 2.1.2延迟脚本
- defer="defer",这个属性告诉浏览器，脚本立即下载，但是延迟到整个页面解析完毕再执行（浏览器遇到</html>这个标签才会执行脚本）
```javascript
<script type="text/javascript" defer="defer" src="1.js"></scrpt>
<script type="text/javascript" defer="defer" src="2.js"></scrpt>
```
- html规范：上面的script标签里面都有defer属性，h5规定要求脚本按照他们出现的先后顺序执行，因此1.js会早于2.js.**但是实际中不是这样，所以最好只包含一个**

-defer属性只用于外链脚本，所以最好的方式还是将脚本放在html尾部 


##### 2.1.3异步脚本
- H5定义的async。只适用于外链脚本，并告诉浏览器立即下载文件。但与defer不同的是，async不保证脚本按照引入顺序的先后执行。

- async的目的不让页面等待两个脚本下载和执行，从而异步加载页面其他内容，因而不要在async里面引入修改dom元素的脚本。
- async一定会load之前执行，但不确定在DOMContentLoaded之前还是之后


#### 2.3文档模式
- 混合模式：如果没有文档声明，所有的浏览器都会默认开启混合模式
- 标准模式 

#### 2.4noscript标签
- 用于不支持javascript的浏览器中显示内容。这个元素可以包含出现在body里面的任何html元素--<script>除外

- noscript在下面的情况下才会显示出来
	- 浏览器不支持脚本
	- 浏览器支持脚本，但是被禁用

- 脚本无效的情况下提示用户
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
</head>
<body>
	<noscript>
		<p>本页面需要浏览器支持(启用)javascript</p>
	</noscript>
</body>
</html>
```