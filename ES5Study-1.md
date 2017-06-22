---
title: javascript菜鸟教程复习
date: 2017-06-22 08:40:40
categories: 前端
tags: [javascript]
---
<Excerpt in index | 首页摘要> 

<!-- more -->
<The rest of contents | 余下全文>

-----

网址：http://www.runoob.com/js/js-tutorial.html
----
#### 1.javascript 输出
##### 1.1javascript显示数据
- window.alert()弹出警告框
- document.write()将内容写入到html，页面内容全部被替换
- 使用innerHTML写入到html元素中，与document.write的区别就是这个可以准确的修改某个dom

- console.log()写入到浏览器控制台


#### 2.javascript 语法

##### 2.1javascript对于大小写敏感
document.getElementById与document.getElementByID两个是不同的

##### 2.2 javascript 的数据类型
布尔型、空类型、字符串、数字、数组、对象、等

对代码进行折行
document.write("你
\好");
这样代码不会报错


##### 2.3 javascript变量
- 变量必须以字母开头
- 变量也可以以$和_开头
- 变量对大小写敏感

变量用var关键字声明


一条语句多个变量，使用逗号分割变量即可
```javascript
	<<script>
		var name="jarry",
		    age=12,
		    city="河北";
	</script>
```

变量只是声明没有赋值`var carname`,这个时候，carname的值是undefined


#### 2.javascript 数据类型
字符串(String)/布尔型(Boolean)/空类型(Null)/未定义(Undefined)/对象(Object)/数组(Array)/数字(Number)

##### javascript 数组
声明方式1
```javascript
<script>
var cars=new Array();
cars[0]="宝马";
cars[1]="奔驰";
cars[2]="沃尔沃";
console.log(cars);
</script>
```

2	`var cars=new Array("奔驰","宝马","大众");`

3  `var cars=["奔驰","宝马","大众"];`


##### javascript 对象
对象由花括号分割，在括号内部以键值对的形式存在(name:value),属性由逗号进行分割

```javascript
var person={
	name:"李明",
	age:23,
	home:"河北"
};
//document.write(person.name);
document.write(person["name"]);

```

##### 变量的声明
- var a=new String;
- var numberValue=new Number;
- var booleanValue=new Boolean;
- var arrayValue=new Array;
- var persion=new Object;


#### 3.对象
```javascript
var person={
	name:"李明",
	age:23,
	home:"河北",
	introduce:function(){
		return "我叫"+this.name+"今年"+this.age+"来自"+this.home;
	},
};
document.write(person.introduce());
```


#### 4.函数
在使用 return 语句时，函数会停止执行，并返回指定的值
```javascript
sayHi();
function sayHi(name,message){
	document.write("return 语句执行前。");
	return;
	alert("hello" + name +"," + message);//这一行永远不会被调用
}
```

作用域
- 局部变量：在函数中通过var声明的变量。
- 全局变量：在函数外通过var声明的变量。
- 没有声明就使用的变量，默认为全局变量，不论这个变量在哪被使用。


#### 5.事件
- onchange
- onclick
- onload
- onmouseover
- onmouseout
- onkeydown


#### 6.字符串,字符串对象
字符串长度
```
	var x="abcdefgh";
	console.log(x.length);//8
	console.log(x[1]);//b
```

特殊字符：反斜杠\

字符串可以是对象
```javascript
<script>
	var x="abcdefgh";
	var y=new String("abcdefgh");
	console.log(typeof(x));//string
	console.log(typeof(y));//object
	console.log(x==y);//true
	console.log(x===y);//false
</script>
```

##### 6.1字符串的属性和方法
原始字符串，例如"hahah"没有属性和方法，应为他们不是对象
原始值可以使用js的属性和方法，因为js在执行方法和属性的时候可以吧原始值当做对象

**字符串属性**
- constructor:返回创建字符串属性的函数
- length:返回字符串长度
- prototype：原型。可以添加属性和方法

**方法**
- charAt():返回指定索引位置的字符
```
var x="abcdefg";
x.charAt(0);
//a
```

- charCodeAt():返回指定索引位置的Unicode值
```javascript
x.charCodeAt(2)
//98
```
- fromeCharCode():将Unicode值转换为字母
```
var n=String.fromCharCode(98);
//b
```

- concat():连接两个或者多个字符串，返回连接后的字符串

```
var y="123"
x.contcat(y);
//abcdefg123
```

- indexOF():返回某个指定的字符串在字符串中首次出现的位置

```
x.indexOf("b")
//1
```

- match():在字符串中检索指定的值，找到一个或者多个正则表达式的匹配

注意： match() 方法将检索字符串 String Object，以找到一个或多个与 regexp 匹配的文本。这个方法的行为在很大程度上有赖于 regexp 是否具有标志 g。如果 regexp 没有标志 g，那么 match() 方法就只能在 stringObject 中执行一次匹配。如果没有找到任何匹配的文本， match() 将返回 null。否则，它将返回一个数组，其中存放了与它找到的匹配文本有关的信息。

```
var x="hahakjiojmjjhajkjhajcakha";
x.match(/ha/);
//["ha", index: 0, input: "hahakjiojmjjhajkjhajcakha"]
x.match(/ha/g);
// ["ha", "ha", "ha", "ha", "ha"]
```

- replace(searchValue,newValue):用于在字符串中用一些字符串替换另一些字符串，或替换一个与正则表达式匹配的子串
```
var x="aaaaaaaAA";
x.replace("a","b");
//"baaaaaaAA"
x.replace(/a/g,"b");
//"bbbbbbbAA"
x.replace(/a/gi,"b");
//"bbbbbbbbb"
```
g：全部替换。   gi:不区分大小写

- search():用于检索字符串中指定的子字符串，或者检索与正则表达式匹配的子字符串，如果没有找到，则返回-1,找到了就返回首次搜索到的脚标
```
var x="aaaaaaaAA"
x.search("m");
//-1
x.search("A");//这样是区分大小写的
//7
x.search(/A/i);//这是不区分大小写，第一个就是
//0
```

- slice(start，end) 提取字符串的片段，并在新的字符串中返回被提取的部分,包含start不包括end，如果没有指定end,则返回在start开始往后的所有字符。start与end可以是负数，只给一个参数，则返回倒数的这个数一直到结尾,如下面的x.slice(-3),返回的是后三位；如果给定两个数，如x.slice(-3,-2)，则返回区间里面的值
```
var x="abcdefg"
x.slice(0,2);
//"ab"
x.slice(-3)
//"efg"
x.slice(-3,-2)
//"e"
```

- split():用于把一个字符串分割成一个字符串数组，如果split("")的话，那么stringObject的每个字符之间都会被分割，注意split方法不改变原来的字符串

```javascript
var x="abcdefg"
x.split("");
 //["a", "b", "c", "d", "e", "f", "g"]

var y="how are you"
y.split("");
//["h", "o", "w", " ", "a", "r", "e", " ", "y", "o", "u"]
y.split(" ");
//["how", "are", "you"]



var y="amdajkjgadkkal"
y.split("a");
//["", "md", "jkjg", "dkk", "l"]
```

- substr(start,length):从脚标为start的位置提取length长度的字符串，包含start脚标，如果没有指明length，则包括脚标start后面的全部，注意与slice的不同

```
var x="abcdefg"
x.substr(1,2)
//"bc"
x.substr(1)
//"bcdefg"
```

- substring(from,to):用于提取字符串中介于两个指定字符串之间的字符，包括开始不包括结束处的字符.frome和to都是非负数，如果to省略，则返回from后面的全部

```
x.substring(1,2)
"b"
x.substring(1)
"bcdefg"
```