---
title: javascript菜鸟教程复习(三)
date: 2017-07-18 09:02:40
categories: 前端
tags: [javascript]
---
<Excerpt in index | 首页摘要> 
javascript菜鸟教程复习(三)
<!-- more -->
<The rest of contents | 余下全文>

-----

网址：http://www.runoob.com/js/js-void.html
此部分代码在：https://github.com/Gabrielkaliboy/demo/tree/master/_posts/ES5Study-3

### 1.javascript：void(0)
javascript:void(0) 中最关键的是 void 关键字， void 是 JavaScript 中非常重要的关键字，该操作符指定要计算一个表达式但是不返回值。
eg1:常用语a标签的死链接
```javascript
 <a href="javascript:void(0)">不会有反应</a>
```

eg2:弹出警告
```javascript
<a href="javascript:void(alert('哈哈哈'))">我会弹出警告窗口</a>
```

#### href="#"与href="javascript:void(0)"的区别
`#` 包含了一个位置信息，默认的锚是#top 也就是网页的上端。而javascript:void(0), 仅仅表示一个死链接。在页面很长的时候会使用 # 来定位页面的具体位置，格式为：# + id。如果你要定义一个死链接请使用 javascript:void(0) 。

### 2.javascript代码规范
#### 变量名
推荐使用驼峰法命名

#### 空格与运算符
通常运算符（=+-*/）前后要有空格
```javascript
var x = y + z;
var values = ["Volvo", "Saab", "Fiat"];
```

#### 代码缩进
通常使用四个空格字符来缩进代码块
```javascript
function toCelsius(fahrenheit) {
    return (5 / 9) * (fahrenheit - 32);
}
```
**不推荐使用 TAB 键来缩进，因为不同编辑器 TAB 键的解析不一样。**


#### 语句规则
简单语句的通用规则：一条语句常以分号作为结束符号
```javascript
var values = ["Volvo", "Saab", "Fiat"];

var person = {
    firstName: "John",
    lastName: "Doe",
    age: 50,
    eyeColor: "blue"
};
```
复杂语句：
- 将做花括号放在第一行的结尾
- 左花括号前添加一空格
- 将右花括号独立放在一行
- 不要以分号结束一个复杂的声明

函数:
```javascript
function toCelsius(fahrenheit) {
    return (5 / 9) * (fahrenheit - 32);
}
```
循环：
```javascript
for (i = 0; i < 5; i++) {
    x += i;
}
```
条件语句：
```javascript
if (time < 20) {
    greeting = "Good day";
} else {
    greeting = "Good evening";
}
```
#### 对象规则
- 将左花括号与类型放在同一行
- 冒号与属性值之间有空格
- 字符串使用双引号，数字不需要
- 最后一个属性值后面不需要添加逗号
- 将右花括号独立的放在一行，并以分号作为结束符号

```javascript
var person = {
    firstName: "John",
    lastName: "Doe",
    age: 50,
    eyeColor: "blue"
};
```
短对象可以直接写成一行
```javascript
var person = {firstName:"John", lastName:"Doe", age:50, eyeColor:"blue"};
```

#### 每行代码字符小于80
为了便于阅读每行字符建议小于数 80 个。如果一个 JavaScript 语句超过了 80 个字符，建议在 运算符或者逗号后换行。

#### 命名规则
- 变量和函数为驼峰法（ camelCase）
- 全局变量未大写UPPERCASE
- 常量，如PI,为大写UPPERCASE

#### 使用小写文件名
大多 Web 服务器 (Apache, Unix) 对大小写敏感： london.jpg 不能通过 London.jpg 访问。其他 Web 服务器 (Microsoft, IIS) 对大小写不敏感： london.jpg 可以通过 London.jpg 或 london.jpg 访问。你必须保持统一的风格，我们建议统一使用小写的文件名。

## 函数
### 3.函数声明
函数声明以后不会立即执行，不调用不执行
```javascript
function myFunction(a, b) {
    return a * b;
}
```
分号是用来分割可执行javascript语句的。由于函数声明不是一个可执行语句，所以**不可以分号结束**。

### 4.函数表达式
函数可以通过一个表达式定义。函数表达式可以存储在变量中
```javascript
var x=function(a,b){return a+b};
```
上面的函数表达式存储在变量里面以后，变量也可以作为一个函数使用
```javascript
var x=function(a,b){return a+b};
var y=x(1,2);
```
上面的函数其实是一个匿名函数。函数存储在变量中，不需要函数名称，通常通过变量名来调用

### 5.函数的提升
函数可以在声明之前调用，但是**用表达式定义函数的时候，无法在声明前使用**
```javascript
    //aa可以调用成功，但是bb会报错，bb is not a function
    console.log(aa(1,2));
    console.log(bb(3,4));
    function aa(a,b){
        return a+b;
    }
    var bb=function(a,b){
        return a*b;
    }
```
### 补充函数变量提升
**重点理解声明、初始化和赋值**
javascript中，函数及变量的声明都将被提升到函数的最顶部；javascript中，变量可以在使用后声明，也就是变量可以先使用，后声明。eg1和eg2效果一样。
**函数声明和变量声明总是会被解释器悄悄地被"提升"到方法体的最顶部。**
```javascript
    x=5;//变量x设置为5
    alert(x);//调用
    var x;//声明x

    var y;//声明
    y=10;//赋值
    alert(y);//调用
```

#### 初始化不会提升
javascript只有声明的变量会提升，初始化的变量不会。下面的结果不同
```javascript
    var x=1;//初始化x
    var y=10;//初始化y
    console.log(x+y);//11

    var z=2;//初始化z
    console.log(z+m);//返回NaN,因为m的值为undefined
    var m=10;//初始化m
```

### 6.自调用函数
- 函数声明的可以自己调用
- 通过表达式定义的函数不能够自己调用自己
```javascript
(function(){
    console.log(1)
})()
```
上面这个执行没有问题，下面这个就会报错了
```
(var x=function(){console.log(1)})()
```

### 7.函数是对象
在 JavaScript 中使用 typeof 操作符判断函数类型将返回 "function" 。但是JavaScript 函数描述为一个对象更加准确。JavaScript 函数有 属性 和 方法。arguments.length 属性返回函数调用过程接收到的参数个数：
```
    function haha(a,b){
        console.log(arguments.length);
    }
    haha();//当前没有传入参数，所以是0
    haha(2,3,4);//传了3,所以是3
```

### 8.函数参数
#### 函数显式参数(Parameters)与隐式参数(Arguments)
```javascript
functionName(parameter1, parameter2, parameter3) {
    // 要执行的代码……
}
```
函数显示参数在函数定义的时候列出。
函数隐式参数在函数调用的时候传递给函数真正的值。

#### 默认参数
如果函数在调用时未提供隐式参数，参数会默认设置为： undefined.有时这是可以接受的，但是建议最好为参数设置一个默认值：
```javascript
    function aa(a,b){
        console.log(a);
        console.log(b);
    }
    aa(1);//这时候只传入了一个参数，所以b为undefined
```

改进
```javascript
    function bb(a,b){
        if(b===undefined){
            b=0;
        }
        console.log(a);
        console.log(b);
    }
    bb(2);

    //改进bb函数
    function cc(a,b){
        y=y || 0;
        console.log(a);
        console.log(b);
    }
    cc(3);
```

#### arguments对象
arguments对象包含了函数调用时候的参数数组

eg:寻找参数里面最大的
```javascript
    function max(){
        var i,
        max=arguments[0];
        if (arguments.legnth<2){
            return max;
        }
        for(i=0;i<arguments.length;i++){
            max > arguments[i] ? max : max = arguments[i];
        }
        return max;
    }
    var max=max(34,45,12,56,4,5,765,34,56,756);
    console.log(max);//返回756
```

### 8.函数调用
js有四种函数的调用方式，每种的区别在于this的初始化

####　8.1this
this指向函数执行时的当前对象

#### 8.2作为一个函数调用
就是我们平时的调用
```javascript
function myFunction(a, b) {
    return a * b;
}
myFunction(10, 2);           // myFunction(10, 2) 返回 20
```

以上函数不属于任何对象。但是在 JavaScript 中它始终是默认的全局对象。这个函数会自动变为window对象的函数。可以在控制台试试myFuntion()与window.myFunction是一样的。

所以说这么写的函数不好。全局的变量，方法或函数容易造成命名冲突的bug

#### 8.3全局对象
当函数没有被自身的对象调用的时候，this的值就会变成全局对象。在web浏览器中，全局对象是浏览器窗口（window对象）
```javascript
function myfun (){
    console.log(this);
    //返回window
}
myfun();
```
函数作为全局对象调用,会使this的值变为全局对象(window)。使用window对象作为一个变量容易造成程序崩溃。

#### 8.4函数作为方法调用
将函数定义为对象的方法
```javascript
var myObject = {
    name:"李明",
    age:"23",
    message:function(){
        return this.name+"  "+this.age+"岁";
    }
};
//调用
console.log(myObject.message());
//myObjcet 是message方法的所有者，函数作为对象的方法调用，会使得this指向对象本身
```
函数作为对象的方法调用，会使得this指向对象本身

#### 8.5使用构造函数调用函数
如果函数调用前使用了 new 关键字, 则是调用了构造函数。构造函数的调用会创建一个新的对象。新对象会继承构造函数的属性和方法。构造函数中 this 关键字没有任何的值(或者是全局的window)。this 的值在函数调用时实例化对象(new object)时创建。
```javascript
function myFunc(name,age){
    this.age=age;
    this.name=name;
    //在没有new对象的时候，this为window，初始化以后就是指向那个实例了
    //console.log(this);
}
var yourFunc=new myFunc("李明",12);
console.log(yourFunc.age);
```
#### 8.6作为函数方法调用函数
js中，函数是对象，他有自己的属性和方法。call和apply都是预定义的属性和方法.两个方法可以用于调用函数,两个方法的第一个参数必须是对象本身。
```javascript
function test(a,b){
    return a+b;
}
var myTest1=test.call(myTest1,2,3);
var myTest2=test.apply(myTest2,[2,3]);
//返回都是5，注意call和apply写法的区别
console.log(myTest1);
console.log(myTest2);
```
两个方法都使用了对象本身作为第一个参数。 两者的区别在于第二个参数： apply传入的是一个参数数组，也就是将多个参数组合成为一个数组传入，而call则作为call的参数传入（从第二个参数开始）。
在 JavaScript 严格模式(strict mode)下, 在调用函数时第一个参数会成为 this 的值， 即使该参数不是一个对象。
在 JavaScript 非严格模式(non-strict mode)下, 如果第一个参数的值是 null 或 undefined, 它将使用全局对象替代。

### 9.闭包
JavaScript 变量可以是局部变量或全局变量。私有变量可以用到闭包。子可以访问父作用域，父不可以访问子作用域变量