---
title: 前端冷知识
date: 2017-06-25 09:10:40
categories: 前端
tags: [前端]
---
<Excerpt in index | 首页摘要> 
前端冷知识
<!-- more -->
<The rest of contents | 余下全文>

-----
只是做个记录，怕丢，详细看这里[点我](http://www.cnblogs.com/Wayou/p/things_you_dont_know_about_frontend.html)

# javascript
### 1.浏览器地址栏运行JavaScript代码
```javascript
javascript:alert('hello from address bar :)');
```
将以上代码贴到浏览器地址栏回车后alert正常执行,注意地址栏不要有别的字符。如果是通过copy paste代码到浏览器地址栏的话，IE及Chrome会自动去掉代码开头的javascript:，所以需要手动添加起来才能正确执行，而Firefox中虽然不会自动去掉，但它根本就不支持在地址栏运行JS代码


### 2.浏览器地址栏运行HTML代码
```javascript
data:text/html,<h1>Hello, world!</h1>
```
#### 2.1基于HTML5的contenteditable属性让页面可编辑
把这扔进浏览器地址栏，回车，页面就可以像notepad一样编辑
```
data:text/html, <html contenteditable>
```

#### 2.2编辑页面中任何东西
```javascript
document.body.contentEditable='true';
```
### 3.利用a标签自动解析URL
很多时候我们有从一个URL中提取域名，查询关键字，变量参数值等的需要，而万万没想到可以让浏览器方便地帮我们完成这一任务而不用我们写正则去抓取。方法就在JS代码里先创建一个a标签然后将需要解析的URL赋值给a的href属性，然后就得到了一切我们想要的了。
```javascript
var a = document.createElement('a');
 a.href = 'http://www.cnblogs.com/wayou/p/';
 console.log(a.host);
```

利用这一原理，稍微扩展一下，就得到了一个更加健壮的解析URL各部分的通用方法了。下面代码来自[James的博客](https://j11y.io/javascript/parsing-urls-with-the-dom/)。
```javascript
function parseURL(url) {
    var a =  document.createElement('a');
    a.href = url;
    return {
        source: url,
        protocol: a.protocol.replace(':',''),
        host: a.hostname,
        port: a.port,
        query: a.search,
        params: (function(){
            var ret = {},
                seg = a.search.replace(/^?/,'').split('&'),
                len = seg.length, i = 0, s;
            for (;i<len;i++) {
                if (!seg[i]) { continue; }
                s = seg[i].split('=');
                ret[s[0]] = s[1];
            }
            return ret;
        })(),
        file: (a.pathname.match(//([^/?#]+)$/i) || [,''])[1],
        hash: a.hash.replace('#',''),
        path: a.pathname.replace(/^([^/])/,'/$1'),
        relative: (a.href.match(/tps?://[^/]+(.+)/) || [,''])[1],
        segments: a.pathname.replace(/^//,'').split('/')
    };
}
```
使用方法
```javascript
var myURL = parseURL('http://abc.com:8080/dir/index.html?id=255&m=hello#top');
 
myURL.file;     // = 'index.html'
myURL.hash;     // = 'top'
myURL.host;     // = 'abc.com'
myURL.query;    // = '?id=255&m=hello'
myURL.params;   // = Object = { id: 255, m: hello }
myURL.path;     // = '/dir/index.html'
myURL.segments; // = Array = ['dir', 'index.html']
myURL.port;     // = '8080'
myURL.protocol; // = 'http'
myURL.source;   // = 'http://abc.com:8080/dir/index.html?id=255&m=hello#top'
```
### 4.页面拥有ID的元素会创建全局变量
在一张HTML页面中，所有设置了ID属性的元素会在JavaScript的执行环境中创建对应的全局变量，这意味着document.getElementById像人的阑尾一样显得多余了。但实际项目中最好老老实实该怎么写就怎么写，毕竟常规代码出乱子的机会要小得多。
```javascript
<div id="sample"></div>
<script type="text/javascript">
        console.log(sample);
</script>
```

### 5.加载CDN文件时，可以省掉HTTP标识
现在很流行的CDN即从专门的服务器加载一些通用的JS和CSS文件，出于安全考虑有的CDN服务器使用HTTPS方式连接，而有的是传统的HTTP，其实我们在使用时可以忽略掉这个，将它从URL中省去。
```javascript
<script src="//domain.com/path/to/script.js"></script>
```

### 6.利用script标签保存任意信息
将script标签设置为type='text'然后可以在里面保存任意信息，之后可以在JavaScript代码中很方便地获取。
```javascript
<script type="text" id="template">
	<h1>This won't display</h1>
</script>
var text = document.getElementById('template').innerHTML
```
### 7. 整数的操作(非常棒！)
JavaScript中是没有整型概念的，但利用好位操作符可以轻松处理，同时获得效率上的提升。

|0和~~是很好的一个例子，使用这两者可以将浮点转成整型且效率方面要比同类的parseInt,Math.round 要快。在处理像素及动画位移等效果的时候会很有用。性能比较[见此](https://jsperf.com/math-floor-vs-math-round-vs-parseint/42)。

```javascript
var foo = (12.4 / 4.13) | 0;//结果为3
var bar = ~~(12.4 / 4.13);//结果为3
```
顺便说句，!!将一个值方便快速转化为布尔值 !!window===true 。

### 8.重写原生浏览器方法以实现新功能
重写浏览器的alert让它可以记录弹窗的次数。
```javascript
(function() {
    var oldAlert = window.alert,
        count = 0;
    window.alert = function(a) {
        count++;
        oldAlert(a + "\n You've called alert " + count + " times now. Stop, it's evil!");
    };
})();
alert("Hello World");
```
### 9.重写console.log() 恶作剧
Chrome的console.log是支持对文字添加样式的，甚至log图片都可以。于是可以重写掉默认的log方法，把将要log的文字应用到CSS的模糊效果，这样当有人试图调用console.log()的时候，出来的是模糊不清的文字。
```javascript
var _log = console.log;
console.log = function() {
  _log.call(console, '%c' + [].slice.call(arguments).join(' '), 'color:transparent;text-shadow:0 0 2px rgba(0,0,0,.5);');
};
```
### 10.不声明第三个变量的值交换(略屌)
说白了就是利用数组
```javascript
var a=1,b=2;a=[b,b=a][0];
```

### 11.万物皆对象
在JavaScript的世界，万物皆对象。除了null和undefined，其他基本类型数字，字符串和布尔值都有对应有包装对象。对象的一个特征是你可以在它身上直接调用方法。对于数字基本类型，当试图在其身上调用toString方法会失败，但用括号括起来后再调用就不会失败了，内部实现是用相应的包装对象将基本类型转为对象。所以(1).toString()相当于new Number(1).toString()。因此，你的确可以把基本类型数字，字符串，布尔等当对象使用的，只是注意语法要得体。

同时我们注意到，JavaScript中数字是不分浮点和整形的，所有数字其实均是浮点类型，只是把小数点省略了而以，比如你看到的1可以写成1.，这也就是为什么当你试图1.toString()时会报错，所以正确的写法应该是这样：1..toString()，或者如上面所述加上括号，这里括号的作用是纠正JS解析器，不要把1后面的点当成小数点。内部实现如上面所述，是将1.用包装对象转成对象再调用方法。

If语句的变形

### 12.If语句的变形
当你需要写一个if语句的时候，不妨尝试另一种更简便的方法，用JavaScript中的逻辑操作符来代替。
```javascript
var day=(new Date).getDay()===0;
//传统if语句
if (day) {
	alert('Today is Sunday!');
};
//运用逻辑与代替if
day&&alert('Today is Sunday!');
```
比如上面的代码，首先得到今天的日期，如果是星期天，则弹窗，否则什么也不做。我们知道逻辑操作存在短路的情况，对于逻辑与表达式，只有两者都真才结果才为真，如果前面的day变量被判断为假了，那么对于整个与表达式来说结果就是假，所以就不会继续去执行后面的alert了，如果前面day为真，则还要继续执行后面的代码来确定整个表达式的真假。利用这点达到了if的效果。

对于传统的if语句，如果执行体代码超过了1 条语句，则需要加花括号，而利用逗号表达式，可以执行任意条代码而不用加花括号。
```
if(conditoin) alert(1),alert(2),console.log(3);
```
上面if语句中，如果条件成立则执行三个操作，但我们不需要用花括号将这三句代码括起来。当然，这是不推荐的，这里是冷知识课堂:)代码可读性太差

### 13.禁止别人以iframe加载你的页面
```javascript
if (window.location != window.parent.location) window.parent.location = window.location;
```



# css
### 去除页面鼠标
```css
*{
    cursor: none!important;
}
```

### 文字模糊效果
```css
p {
    color: transparent;
    text-shadow: #111 0 0 5px;
}
```
### 垂直居中
利用了translate来巧妙实现了垂直居中样式，需IE9+。
```css
.center-vertical {
    position: relative;
    top: 50%;
    transform: translateY(-50%);
}
```
相比而言，水平居中要简单得多，像上面提到的text-align:center，经常用到的技巧还有margin:0 auto。但对于margin大法也只在子元素宽度小于容器宽度时管用，当子元素宽度大于容器宽度时此法失效。

如法炮制，利用left和transform同样可实现水平居中，不过意义不大，毕竟text-align和margin差不多满足需求了
```css
.center-horizontal {
    position: relative;
    left: 50%;
    transform: translateX(-50%); 
}
```
### 多重边框

利用重复指定box-shadow来达到多个边框的效果
```css
/*CSS Border with Box-Shadow Example*/
div {
    box-shadow: 0 0 0 6px rgba(0, 0, 0, 0.2), 0 0 0 12px rgba(0, 0, 0, 0.2), 0 0 0 18px rgba(0, 0, 0, 0.2), 0 0 0 24px rgba(0, 0, 0, 0.2);
    height: 200px;
    margin: 50px auto;
    width: 400px
}
```
### 实时编辑CSS
通过设置style标签的display:block样式可以让页面的style标签显示出来，并且加上contentEditable属性后可以让样式成为可编辑状态，更改后的样式效果也是实时更新呈现的。此技巧在IE下无效。拥有此技能者，逆天也！
```css
<!DOCTYPE html>
<html>
    <body>
        <style style="display:block" contentEditable>
        	body { color: blue }
        </style>
    </body>
</html>
```
### 创建长宽比固定的元素
通过设置父级窗口的padding-bottom可以达到让容器保持一定的长度比的目的，这在响应式页面设计中比较有用，能够保持元素不变形。
```css
<div style="width: 100%; position: relative; padding-bottom: 20%;">
    <div style="position: absolute; left: 0; top: 0; right: 0; bottom: 0;background-color:yellow;">
        this content will have a constant aspect ratio that varies based on the width.
    </div>
</div>
```
### CSS中也可以做简单运算
通过CSS中的calc方法可以进行一些简单的运算，从而达到动态指定元素样式的目的。
```css
.container{
	background-position: calc(100% - 50px) calc(100% - 20px);
}
```