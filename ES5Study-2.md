---
title: javascript菜鸟教程复习(二)
date: 2017-06-23 08:40:40
categories: 前端
tags: [javascript]
---
<Excerpt in index | 首页摘要> 

<!-- more -->
<The rest of contents | 余下全文>

-----

网址：http://www.runoob.com/js/js-tutorial.html

#### 1.typeof
```html
typeof "John"                // 返回 string 
typeof 3.14                  // 返回 number
typeof false                 // 返回 boolean
typeof [1,2,3,4]             // 返回 object
typeof {name:'John', age:34} // 返回 object
typeof null                  //返回object
typeof NaN                   //返回number
typeof myCar                  //undefined，因为没有定义
typeof new Date()             //返回object
```
如果对象是 JavaScript Array 或 JavaScript Date ，我们就无法通过 typeof 来判断他们的类型，因为都是 返回 Object。

1. 可以设置null来清空对象

```
var persion=null;//值为null(空)，但是类型为对象
```
2. 设置undefined来清空对象

```javascript
var person = undefined;     // 值为 undefined, 类型为 undefined
```

3. null与undefined的区别

```javascript
typeof undefined             // undefined
typeof null                  // object
null === undefined           // false
null == undefined            // true
```

4. construction属性：返回所有的javascript变量的构造函数

```html
"John".constructor                 // 返回函数 String()  { [native code] }
(3.14).constructor                 // 返回函数 Number()  { [native code] }
false.constructor                  // 返回函数 Boolean() { [native code] }
[1,2,3,4].constructor              // 返回函数 Array()   { [native code] }
{name:'John', age:34}.constructor  // 返回函数 Object()  { [native code] }
new Date().constructor             // 返回函数 Date()    { [native code] }
function () {}.constructor         // 返回函数 Function(){ [native code] }
```
eg：可以使用instruction可以查看对象是否为数组（是否包含字符串array）
```javascript
function isArray(myArray){
	return myArray.constructor.toString().indexOf("Array")>-1;
};
```

5. 类型转换

```javascript
String(x)         // 报错未定义
String(123)       // 将数字 123 转换为字符串并返回"123"
String(100 + 23)  // 将数字表达式转换为字符串并返回"123"
```
上面的代码相当于使用
`(123).toString()`

转换布尔值
```javascript
String(false)        // 返回 "false"
String(true)         // 返回 "true"
```

转换日期
```javascript
String(Date())      // 返回 Thu Jul 17 2014 15:38:19 GMT+0200 (W. Europe Daylight Time)
```

6. +号，强制类型转换

```javascript
var y = "5";      // y 是一个字符串
var x = + y;      // x 是一个数字
typeof x    "number"
```
如果变量不能转换，它仍然会是一个数字，但值为 NaN (不是一个数字):
```javascript
var y = "John";   // y 是一个字符串
var x = + y;      // x 是一个数字 (NaN)
```

7. 布尔值转换为数字

```javascript
Number(false) //0
Number(true)  //1
```

8. 日期转为数字

```javascript
var d=new Date
//Fri Jun 23 2017 10:24:22 GMT+0800 (中国标准时间)
Number(d)
//1498184662219
//和Date的getTime()方法效果是一样的
d.getTime()  
//1498184662219
```

9. 自动类型转换

```javascript
5 + null    // 返回 5         null 转换为 0
"5" + null  // 返回"5null"   null 转换为 "null"
"5" + 1     // 返回 "51"      1 转换为 "1"  
"5" - 1     // 返回 4         "5" 转换为 5
```


#### 2.正则表达式

1. 使用字符串的方法

search():用于检索字符串中指定的子字符串，或检索与正则表达式相匹配的子字符串，并返回子串的起始位置，没有就返回-1
```javascript
var x="hello zhu";
x.search("zhu")
//6,注意有空格，这是使用的字符串作为子串的

var x="AAAABBBJJOIDDKKOHF"
x.search(/o/i);
//9,这里的参数i是说不区分大小写
```
replace():用于在字符串中用一些字符替换另一些字符，或替换一个与正则表达式相匹配的子串
```javascript
var x="AAAABBBJJOIDDKKOHF"
x.replace("A","Z");//这样写只替换了第一个匹配到的字符
//"ZAAABBBJJOIDDKKOHF"
x.replace(/A/g,"Z");
//"ZZZZBBBJJOIDDKKOHF"
```



2. 正则表达式修饰符

- i:执行对大小写敏感的匹配
- g:执行全局匹配(查找所有匹配，而不是在找到第一个匹配以后停止)
- m:执行多行匹配


3. 使用test()函数

用于检测一个字符串是否匹配某个模式，如果字符串中含有匹配文本，则返回true，否则返回false
```javascript
var x="AAAABBBJJOIDDKKOHF"
var y=/F/;
y.test(x)
true
```

4. 使用exec() 是正则表达式的一个方法，检测一个字符串是否匹配某个模式，该函数返回一个数组，其中存放匹配的结果，如果没有找到，则返回null

```javascript
var x="AAAABBBJJOIDDKKOHF"
var y=/A/g
y.exec(x);
["A", index: 0, input: "AAAABBBJJOIDDKKOHF"]0: "A"index: 0input: "AAAABBBJJOIDDKKOHF"length: 1__proto__: Array(0)
```
#### 3.javascript 错误
- try：语句测试代码块的错误
- catch：语句处理错误
- throw：语句创建自定义错误

语法:
```javascript
try {
  //在这里运行代码
} catch(err) {
  //在这里处理错误
}
```
eg
```javascript
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
</head>
<body>
	<p>请输入5-10之间的数字</p>
	<input type="text" id="demo">
	<button type="button" onclick="test()">测试输入</button>
	<p id="message"></p>
</body>
<script>
function test(){
	var message,x;
	//错误信息显示的地方
	message=document.getElementById("message");
	//每次点击按钮清空错误信息
	message.innerHTML="";
	//获取用户输入
	x=document.getElementById("demo").value
	try{
		if(x==""){
			throw "值为空"
		}
		if(isNaN(x)){
			throw "不是数字"
		}
		x=Number(x);
		if(x<5){
			throw "太小"
		}
		if(x>10){
			throw "太大"
		}
	}catch(error){
		message.innerHTML="错误：" +error
	}
};
</script>
</html>
```
#### 4.严格模式
```javascript
"use strict";
myFunction();

function myFunction() {
    y = 3.14;   // 报错 (y 未定义)
}
```

#### 5. javascript使用误区
##### 5.1 赋值运算符应用错误在 :JavaScript 程序中如果你在 if 条件语句中使用赋值运算符的等号 (=) 将会产生一个错误结果, 正确的方法是使用比较运算符的两个等号 (==)。

- 正常写法，if条件返回false，因为0不等于10
```javascript
var x=0;
if(x==10)
```

- 错误写法,这时候的if后面返回的是true，因为x被重新赋值为10了，会被强制转换为true,这和我们本意是不一样的

```javascript
var x=0
if(x=10){}
```

- 错误写法,这时候我们的本意是当x=0的时候执行后面的语句，结果if后面的x=0直接给赋值了，0会被强制转为false，导致后面的语句不执行

```javascript
var x=0;
if(x=0){}
```

##### 5.2 比较运算符常见错误：
- 比较运算中，数据类型会被忽略.下面的if返回true

```javascript
var x=10;
var y="10";
if(x==y){}
```

- ===值和类型都相同,下面的if返回false

```javascript
var x=10;
var y="10";
if(x===y){}
```

- switch里面的case使用的恒等计算（====）

下面这个会执行后面的alert
```javascript
var x = 10;
switch(x) {
    case 10: alert("Hello");
}
```

下面这个不会执行,因为switch执行的是恒等
```javascript
var x = 10;
switch(x) {
    case "10": alert("Hello");
}
```

##### 5.3 加号还是连接符号？
+两边只要有一个是字符串，那他就是连接符号


##### 5.4 浮点型数据使用注意事项
所有的编程语言，包括 JavaScript，对浮点型数据的精确度都很难确定：
```javascript
var x = 0.1;
var y = 0.2;
var z = x + y            // z 的结果为 0.3
if (z == 0.3)            // 返回 false
```

为解决上面的问题，可以这么写
```javascript
var z = (x * 10 + y * 10) / 10;       // z 的结果为 0.3
```

##### 5.5字符串分行
正确
```
var x =
"Hello World!";
```
错误
```
var x ="Hello 
World!";
```
需要使用反斜杠\来解决
```
var x = "Hello \
World!";
```

##### 5.6错误使用分号
由于分号使用错误，if 语句中的代码块将无法执行：

```
if (x == 19);
{
    // code block  
}
```

##### 5.7 return使用错误
js默认在最后一行自动结束，一下两个实验结果是一样的（有无分号）
```
function myFunction(a) {
    var power = 10  
    return a * power
}
```

```
function myFunction(a) {
    var power = 10;
    return a * power;
}
```
JavaScript 也可以使用多行来结束一个语句。
以下实例返回相同的结果:
```
function myFunction(a) {
    var
    power = 10;  
    return a * power;
}
```

但是，以下实例结果会返回 undefined：

```
function myFunction(a) {
    var
    power = 10;  
    return
    a * power;
}

```
上面的代码相当于下面的实例
```
function myFunction(a) {
    var
    power = 10;  
    return;       // 分号结束，返回 undefined
    a * power;
}
```
由于 return 是一个完整的语句，所以 JavaScript 将关闭 return 语句。


##### 5.8数组中使用名字来索引
使用名字来作为索引的数组称为关联数组（或哈希）
javascript不支持使用名字来索引，仅允许数字索引
```
var person = [];
person[0] = "John";
person[1] = "Doe";
person[2] = 46;
var x = person.length;         // person.length 返回 3
var y = person[0];             // person[0] 返回 "John"
```


js中，对象可以使用名字来作为索引，但是如果你使用名字作为索引，当访问数组时，JavaScript 会把数组重新定义为标准对象。
执行这样操作后，数组的方法及属性将不能再使用，否则会产生错误

```
var person = [];
person["firstName"] = "John";
person["lastName"] = "Doe";
person["age"] = 46;
var x = person.length;         // person.length 返回 0
var y = person[0];             // person[0] 返回 undefined
```

##### 5.9 定义数组元素和定义对象元素，最后都不能留逗号
以下两个都是错误的
```
points = [40, 100, 1, 5, 25, 10,];
websites = {site:"菜鸟教程", url:"www.runoob.com", like:460,}
``` 

##### 5.9 undefined不是null
在javascript中，null用于对象，undefined用于变量、属性和方法。对象只有被定义才会有可能为null，否则就是undefined。如果我们测试对象是否存在，在对象还没有定义的时候会抛出错误

错误使用
```
if(myObjcet !==null && myObject !=="undefined")
```
正确使用
```
if(myObject !=="undefined" && myObject !==null)
```

根本还是&&机制


##### 5.10代码块的作用域是全局
在每个代码块中 JavaScript 不会创建一个新的作用域，一般各个代码块的作用域都是全局的。
以下代码的的变量 i 返回 10，而不是 undefined：
```
for (var i = 0; i < 10; i++) {
    // some code
}
return i;
```


#### 6. javascript 表单
当用户提交的时候进行验证
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
	<script>
		function validate(){
			var userName=document.forms[0]["userName"].value;
			if(userName==null || userName==""){
				alert("请输入姓名");
				return false;
			}
		};
	</script>
</head>
<body>
	<form action="test.php" method="post" id="myform" name="myform" onsubmit="return validate()">
		<label for="userName">名字：</label><input type="text" id="userName" name="userName">
		<input type="submit" value"提交">
	</form>
</body>
</html>
```

判断用户输入的数字
```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<p>请输入10-20之间的数字</p>
	<form action="test.php" name="myform" id="myform">
		<label for="typeNum">请输入数字:<input type="text" name="typeNum" id="typeNum"></label>
		<input type="button" value="提交" id="btn">
	</form>
	<p id="aa"></p>
</body>
<script>
		var aa=document.getElementById("aa"),
		btn=document.getElementById("btn");
		btn.addEventListener("click",check);
	function check(){
		var typeNum=document.forms["myform"]["typeNum"].value;
		aa.innerHTML="";
		if(isNaN(typeNum)){
			text="请输入数字";
		}
		else if(typeNum==""){
			text="你没有输入任何值"
		}
		else if(typeNum <10){
			text="输入的值小于10";
		}
		else if(typeNum > 20){
			text="输入的值过大";
		}else{
			text=typeNum;
		}
		aa.innerHTML=text;

	};
</script>
</html>
```

html表单自动校验
```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
</head>
<body>
	<form action="1.php" id="myform">
		<label for="userName">请输入姓名：
			<input type="text" name="userName" id="userName" required="required">
		</label>
		<label for="pword">请输入密码：
			<input type="password" name="pword" id="pword" required pattern="[A-Z]{3}" title="只能输入三个大写字母">
		</label>
		<label for="age">请输入年龄：
			<input type="number." name="age" id="age" required pattern="[0-9]" min="10" max="100" title="只能输入数字">
		</label>
		<input type="submit" value="提交">
	</form>
</body>
</html>
```
min和max只可以给type=date和type=number用，pattern里面放的是正则，title是提示

##### 验证约束的dom方法
- checkValidity():如果input里面数据是合法的则返回true，否则返回false
- setCustomValidity():设置input元素的validationMessage属性，用于自定义错误信息提示的方法。使用setCustomValidity()设置了自定义提示以后，validity.customError就会变成true，则checkValidity总是会返回false。如果重新判断，需要取消自定义提示，方式如下：

```html
setCustomValidity("");
setCustomValidity(null);
setCustomValidity(undefined);
```

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
</head>
<body>

<p>输入数字并点击验证按钮:</p>

<input id="id1" type="number" min="100" max="300" required>
<button onclick="myFunction()">验证</button>

<p>如果输入的数字小于 100 或大于300，会提示错误信息。</p>

<p id="demo"></p>

<script>
function myFunction() {
    var inpObj = document.getElementById("id1");
    if (inpObj.checkValidity() == false) {
        document.getElementById("demo").innerHTML = inpObj.validationMessage;
    } else {
        document.getElementById("demo").innerHTML = "输入正确";
    }
}
</script>

</body>
</html>
```

##### 约束验证dom属性
- validity：布尔属性值，返回input输入值是否合法
- validationMessage:浏览器错误提示信息
- willValidate:指定input是否需要验证

##### validity属性
input元素的validity属性包含一系列validity数据属性
- customError：设置为true，如果设置了自定义的validity信息
- patternMismatch：设置为true，如果元素的值不匹配他的模式属性
- rangeOverflow：设置为true，如果元素的值大于设置的最大值
- rangeUnderflow：设置为true，如果元素的值小于设置的最小值
- stepMismatch：设置为true，如果元素的值不按照规定的step属性设置
- tooLong:设置为true，如果元素的值超过了maxLength属性设置的长度
- typeMismatch：设置为true，如果元素的值不是预期相匹配的类型
- valueMissing：设置为true，如果元素（require）没有值
- valid：设置为true，如果元素的值是合法的

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
</head>
<body>

<p>输入数字并点击验证按钮:</p>

<input id="id1" type="number" max="100">
<button onclick="myFunction()">验证</button>

<p>如果输入的数字大于 100 ( input 的 max 属性), 会显示错误信息。</p>

<p id="demo"></p>

<script>
function myFunction() {
    var txt = "";
    if (document.getElementById("id1").validity.rangeOverflow) {
        txt = "输入的值太大了";
    } else {
        txt = "输入正确";
    }
    document.getElementById("demo").innerHTML = txt;
}
</script>

</body>
</html>
```

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
</head>
<body>

<p>输入数字并点击验证按钮:</p>
<input id="id1" type="number" min="100" required>
<button onclick="myFunction()">验证</button>

<p>如果输入的数字小于 100 ( input 的 min 属性), 会显示错误信息。</p>

<p id="demo"></p>

<script>
function myFunction() {
    var txt = "";
	var inpObj = document.getElementById("id1");
	if(!isNumeric(inpObj.value)) {
		txt = "你输入的不是数字";
	} else if (inpObj.validity.rangeUnderflow) {
        txt = "输入的值太小了";
    } else {
        txt = "输入正确";
    }
    document.getElementById("demo").innerHTML = txt;
}

// 判断输入是否为数字
function isNumeric(n) {
    return !isNaN(parseFloat(n)) && isFinite(n);
}
</script>

</body>
</html>
```