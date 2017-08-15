---
title: 前端开发过程中的bug以及兼容性记录（一）
date: 2017-06-27 18:00:40
categories: 前端
tags: [bug记录]
---
<Excerpt in index | 首页摘要> 
前端开发过程中的bug以及兼容性记录（一）
<!-- more -->
<The rest of contents | 余下全文>

-----
源码：https://github.com/Gabrielkaliboy/demo/tree/master/_posts/bugCompatibility-1
### 1.IE浏览器文件上传返回的json会提示你下载
如图
![](https://github.com/Gabrielkaliboy/images/blob/master/_posts/bugCompatibility_1/1.png?raw=true)

解决方式：
根据不同的后台语言进行搜索搜索，关键字
- IE 文件上传返回json
- .net上传返回json

修改一下后台返回的数据类型就可以,将后台返回的json模式修改一下，这个问题里面实在.net的json返回的代码里面强制声明了一下，将json改为了字符串格式，`text/html`

放段代码
```.net
if (reboo > 0)
{
    return Json(new
    {
        error = "",
        operateType = "save",
        dealSuccessFlag = true
    }, "text/html");
}
```


### 2. 360安全浏览器在默认安装打开情况下使用IE7的文档模式导致页面布局乱套问题
百度搜索：360安全浏览器默认IE7

#### 2.1 问题描述
页面在Chrome以及IE9/10/11都没有问题，结果在360安全浏览器下打开以后页面布局乱套了，打开控制台发现，360安全浏览器的默认文档模式是IE7。就是这个根本原因导致我好好的页面错乱！

#### 2.2解决
查了很多资料，最后只有这个起效了。将下面这句话放在header的第一个位置，切记是第一位置,简单粗暴

```html
<meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1">
```
我的代码结构
```html
<head>
    <meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1">
    <meta charset="UTF-8">
    <title>登录(Login)</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" http-equiv="Cache-Control" content="no-cache,must-revalidate">
    <meta name="author" content="0">
    <link rel="stylesheet" href="~/Content/Css/base.css">
    <link rel="stylesheet" href="~/Content/Css/login/style.css">
    <script src="~/Scripts/jquery-1.10.2.js"></script>
    <script type="text/javascript" src="~/Scripts/JS/logIn/scripts.js" charset="utf-8"></script>
</head>
```
**补充**为什么简单粗暴？
- 1.根据官网定义X-UA-compatible 标头不区分大小写；不过，它必须显示在网页中除 title 元素和其他 meta 元素以外的所有其他元素之前。如果不是的话，它不起作用。这么啰嗦，我为了简单，直接放在了header的第一个位置，亲测，可行
- 2.content的内容是IE=8，或者IE=edge等值，注意不是IE8或者直接写个edge的值，否则不起作用。

有人说这个也可以解决，以后可以测试一下
```html
<meta name="renderer" content="webkit|ie-comp|ie-stand">  
```
亲测上面的meta可用，他是在360安全浏览器渲染的时候直接使用chrome模式，但是如果刻意的调到IE兼容，还会乱。第一个方法，不论用户使用哪种模式（极速或者兼容），都能够正常显示。所以还是第一个方法好一些。为了让浏览器自己打开的时候直接是极速模式，我将第一个meta做了修改

```html
<meta http-equiv="X-UA-Compatible" content="Chrome=1,IE=edge" />
```
将Chrome放在了第一个位置，没效果！！！！！！！！！！
#### 2.3知识补充

**关于360浏览器**
360有极速版和安全浏览器，二者都是双核模式（IE的trident和谷歌的webkit）。极速模式默认优先使用Chrome打开页面，只有在银行系统下才会自动切换到IE模式；安全浏览器下载安装以后默认打开是IE兼容模式，也就是我们上面写的IE7兼容模式，很恶心，他还可以在地址栏那里手动切换回极速模式（Chrome）

**参考**
360浏览器内核控制Meta标签说明文档：http://se.360.cn/v6/help/meta.html
360安全浏览器 7.1的遇到的模式切换问题：http://www.binjs.com/archives/1015
Stack Overflow：http://stackoverflow.com/questions/6771258/whats-the-difference-if-meta-http-equiv-x-ua-compatible-content-ie-edge-e


### 3.toFixed在保留小数的同时将类型也变了
本来数据是number类型，经过toFixed以后，变为了string类型，这个有点坑
```javascript
//toFixed
//将一个数值转成字符串，并进行四舍五入，保留指定位数的小数

var num = 11.1234;
var newString = num.toFixed(2);
document.write("type: " + typeof (newString));
document.write(newString);
```

### 4.模拟点击a标签触发页面跳转
有的时候我们想给a标签添加一个点击事件，让他根据其属性href进行跳转
```javascript
<a id="alink" href="1.html" style="visibility: hidden;">下一步</a> 
$("#alink").click(); // 触发了a标签的点击事件，但是没有触发页面跳转 
document.getElementById("alink").click(); //既触发了a标签的点击事件，又触发了页面跳转 
```
如果我们不想使用第二种方法.
把 “下一步” 改为 “<span id="spanId">下一步</span>” 即给A标签中的文字添加一个能被jQuery捕获的元素，然后$("#spanId").click()；，才可以触发页面跳转。


### 5.png图片在Chrome、IE、Firefox、ps中颜色不一致问题
问题描述：公司做了一个logo，结果在ps中是A颜色，IE与ps一样都是A颜色，但是放在Firefox和Chrome中颜色就不一致了。原因在于，png图片保存的时候有一个ICC配置文件，如果勾选这个选项，就会导致这个问题。

关于这个问题的讨论：https://bugs.chromium.org/p/chromium/issues/detail?id=44872
解决方法：不勾选或者直接保存为web所用格式！

### 6.同时使用hover和after/before伪类
有时候有这样的需求，当鼠标划上的时候，显示一个三角

重点：**.applyItemsTabItem:hover::after**后面是两个冒号的after，记得在.applyItemsTabItem里面设置相对定位`position:relative`

![](https://github.com/Gabrielkaliboy/images/blob/master/_posts/bugCompatibility_1/1.gif?raw=true)
```css
.applyItemsTabItem {
    width: 14.285%;
    position:relative;
    float: left;
    text-align: center;
    height: 100px;
    border-bottom: 1px solid #e2d9d9;
    border-left: 1px solid #e2d9d9;
    border-right: 1px solid #e2d9d9;
}
.applyItemsTabItem:hover {
    border-bottom: 3px solid #1D82D2;
}
.applyItemsTabItem:hover::after {
border-bottom:3px solid #1D82D2;
content: '';
position: absolute;
top: 100%;
left: 42%;
width: 0;
height: 0;
border-width: 11px;
border-style: solid;
border-color: transparent;
margin-bottom: 1px;
border-top-color: currentColor;
color: #1D82D2;
}
```

### 7.关于点击按钮显示div,然后点击页面其他区域隐藏div的实现
首先可以给 document 对象绑定 click 事件。
然后由于事件冒泡机制，你单击文档的任意地方（包括绿色区域）都会触发 click 事件。

先在事件里写上隐藏div区域的代码
然后，再给div区域绑定click事件，这时候阻止事件冒泡，这样一来，点击div区域的话，是不会隐藏掉自己的。
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<script src="https://cdn.bootcss.com/jquery/3.0.0/jquery.min.js"></script>
	<style>
		#div1{
			display: none;
		}
	</style>
	<title>Document</title>
</head>
<body>
	<button id="btn">点我显示</button>
	<div id="div1">哈哈哈</div>
</body>
<script>
$(function(){
	$("#btn").on("click",function(e){
		e.stopPropagation();
		$("#div1").css("display","block");
	});
	$(document).on("click",function(e){
		$("#div1").css("display","none");
	});
})
</script>
</html>
```
### 8.meta 标签

#### 8.1
```html
<meta http-equiv="X-UA-Compatible" content="IE=edge"> 
```
关于这个标签在[stack overflow](https://stackoverflow.com/questions/6771258/what-does-meta-http-equiv-x-ua-compatible-content-ie-edge-do)

如果你需要兼容IE9或者IE8，这个标签最好写上，如果只要求最新，比如兼容到IE11或者edge，那可以把它剔除

`X-UA-Compatible`这个meta标签允许开发者设置浏览器以哪个版本的IE来进行渲染 

根据Microsoft的文档说明，这个标签最好是放在header的最顶部，IE浏览器在遇到这个标签的时候，会以最新版本的IE(客户电脑上所带的最新版IE)去渲染HTML。这会导致性能问题，因为浏览器是重新去渲染HTML


### 9. jQuery 1.9 最后支持 IE 6/7/8 的版本

### 10.IE8 缺少标识符、字符串或数字
![](https://github.com/Gabrielkaliboy/images/blob/master/_posts/bugCompatibility_1/2.png?raw=true)

IE早期浏览器对于格式校验比较严，如果出现SCRIPT1028: 缺少标识符、字符串或数字的错误很大可能是因为多了逗号或者分号什么的，比如：

```javascript
var a = {  
    x: 1,  
    y: 2,  
};  
```
y:2后面多了个逗号，这在Firefox或者chrome浏览器及新的IE浏览器都正常，但是IE8以下浏览器是会报错的。直接去掉就可以


**还有一种情况**
```javascript
tool:{  
    const:{  
        phone:XXXXXX  
    }  
     }  
```
问题出在这行代码上，IE8及以下浏览器，不能用const作为json的key