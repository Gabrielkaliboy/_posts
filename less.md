---
title: less学习
date: 2017-06-25 09:10:40
categories: 前端
tags: [less]
---
<Excerpt in index | 首页摘要> 
less学习
<!-- more -->
<The rest of contents | 余下全文>
-----

网址：http://lesscss.cn/
快速入门：http://less.bootcss.com/

#### less	是什么？
类似于jQuery，是一种动态样式语言，属于css预处理语言的一种，它使用类似css语法，为css赋予了动态语言的特性，如变量，继承，运算，函数等，更方便css的编写和维护

#### less的编译环境
浏览器端，桌面客户端，服务器端

#### less编译工具
- koala (考拉)编译
	- koala
	- 国人开发的less/sass编译工具
	- 网址：http://koala-app.com/index-zh.html

- Node.js库
- 浏览器端使用

#### kaola使用
- 将软件设置为中文
	- 设置好了以后，再次打开的时候就是英文了
![](https://github.com/Gabrielkaliboy/images/blob/master/_posts/less/1.gif?raw=true)

- 新建一个项目的工程目录，比如我们叫less文件夹，在style里新建一个 main.less文件
	- 里面有style文件
	- images文件夹等

- 将less文件夹整体拖进kaola，如图所示

![](https://github.com/Gabrielkaliboy/images/blob/master/_posts/less/2.gif?raw=true)

- 设置编译less文件以后的输出路径
![](https://github.com/Gabrielkaliboy/images/blob/master/_posts/less/3.gif?raw=true)

- 执行以下编译，如果显示success，那就是成功了
![](https://github.com/Gabrielkaliboy/images/blob/master/_posts/less/4.gif?raw=true)

- 打开style文件夹，就可以看到main.css文件了，将我们的main.css引入我们相应的html里面就可以用了，写的时候直接在less里面写，他会直接将css生成输出到main.css里面。

- 在koala里面还有一个设置输出的方式，normal表示输出的就是正常的css,compress表示输出压缩以后的css

![](https://github.com/Gabrielkaliboy/images/blob/master/_posts/less/1.png?raw=true) 


#### less注释
- /**/:这个会将注释保留到编译的css文件里面
- //：这个只在当前的less文件里面存在

因为我们以后维护的就是less文件，所以直接用//就行，

#### 变量
声明变量的话，一定要用一个@符号开头，例如：@变量名：变量值；注意后面的分号

```less
//测试变量，我提前声明了test_width的值，用到200px的地方直接写
@test_width:200px;
.box{
    width:@test_width;
}
```
对应输出的css
```css
.box {
  width: 200px;
}
```
不同变量里面的相同的参数是不互相影响的,例如下面的.border里面和.border_1里面是不互相影响的
```less
@charset"utf-8";
//混合可以带参数
.border(@border_width){
    border: @border_width  solid #f0f;
}

.box{
    .border(20px);
}
//混合参数可以是默认值
.border_1(@border_width:10px){
    border:@border_width solid #989;
}
//使用默认值
.box_1{
    .border_1();
}
```

#### 混合
##### 1.基础混合

将一个选择器A里面的样式，直接在另一个选择器B里面写选择器A的名字，他会自动的将A里面的样式，写到B里面A的位置上，看下面代码，说的有点乱
```less
@charset"utf-8";
//测试混合，注意看.box里面的.border,生成的css文件会把.border里面的样式给复制进入.box里面.border的位置上
.box{
    .border;
}

.border{
    border:1px solid #f00;
}
```

生成的css
```css
@charset "utf-8";
.box {
  border: 1px solid #f00;
}
.border {
  border: 1px solid #f00;
}

```

在看一个例子
```less
@charset"utf-8";
//测试混合，注意看.box里面的.border,生成的css文件会把.border里面的样式给复制进入.box里面.border的位置上
.box{
    .border;
    background:#f90;
}

.border{
    border:1px solid #f00;
}
//混合测试，注意查看.box2里面的.box
.box2{
    .box;
    margin-left:12px;
}
```
编译的css
```css
@charset "utf-8";
.box {
  border: 1px solid #f00;
  background: #f90;
}
.border {
  border: 1px solid #f00;
}
.box2 {
  border: 1px solid #f00;
  background: #f90;
  margin-left: 12px;
}

```


##### 2.混合可以带参数
其实目的就是可以动态的更改里面的某个变量，而不是写死了
```less
@charset"utf-8";
//混合可以带参数
.border(@border_width){
    border: @border_width  solid #f0f;
}
//注意这里的参数20px
.box{
    .border(20px);
}
```

生成的css文件
```css
@charset "utf-8";
.box {
  border: 20px solid #ff00ff;
}

```
##### 3.混合可以带参数,参数可以是默认值
带参数的话调用的时候就可以不写,但是如果没有默认值，向上面的一样，就必须写。如果不想使用默认值，在写的时候，直接覆盖就行。**一定要注意带不带括号**
less
```less
@charset"utf-8";
//混合参数可以是默认值
.border_1(@border_width:10px){
    border:@border_width solid #989;
}
//使用默认值
.box_1{
    .border_1();
}
//不使用默认值而是传参
.box_2{
    .border_1(50px);
}
```
css
```css
@charset "utf-8";
.box_1 {
  border: 10px solid #998899;
}
.box_2 {
  border: 50px solid #998899;
}

```


实际开发中的一个应用:border-radius的一个兼容性
less
```less
@charset"utf-8";
.border_radius(@border_width:5px){
    -webkit-border-radius:@border_width;
    -moz-border-radius:@border_width;
    border-radius: @border_width;
}
//记得调用的时候加括号(实际测试中不加括号也可以)
.test_radius{
    .border_radius();
}
```
css
```css
@charset "utf-8";
.test_radius {
  -webkit-border-radius: 5px;
  -moz-border-radius: 5px;
  border-radius: 5px;
}
```


#### 匹配模式
正常的一个三角的样式
```css
//overflow:hidden 是为了处理ie6最小高度问题
.triangle{
    width:0;
    height:0;
    overflow: hidden;

    border-width:10px;
    border-color: transparent   transparent red transparent;
    border-style:  dashed  dashed solid dashed;
}
```
上面的代码，可以根据不同的三角朝向，分为上下左右，我们想写css的时候，简单一些，就用到了匹配模式

less文件
```
//匹配模式，根据下面的输入，匹配不同朝向的三角
//向下的
.sanjiao(bottom,@w:5px,@c:#f0f){
    border-width:@w;
    border-color:@c transparent transparent transparent;
    border-style:solid dashed dashed dashed;
}
//向左的
.sanjiao(left,@w:5px,@c:#f0f){
    border-width:@w;
    border-color: transparent @c transparent transparent;
    border-style: dashed solid dashed dashed;
}
//向上的
.sanjiao(top,@w:5px,@c:#f0f){
    border-width:@w;
    border-color: transparent  transparent  @c transparent;
    border-style: dashed  dashed solid dashed;
}
//向右的
.sanjiao(right,@w:5px,@c:#f0f){
    border-width:@w;
    border-color: transparent  transparent  transparent @c;
    border-style: dashed  dashed dashed solid;
}
//将上下左右里面的公共样式放在这个。上面不管选择的是谁，都得带着我这个样式。@_这是固定写法
.sanjiao(@_,@w:5px,@c:#f0f){
    width:0;
    height:0;
    overflow: hidden;
}
//上面的所有写的东西，都是为了这里的调用，写一个下三角
.triangle{
    .sanjiao(bottom,100px)
}
```

生成的css
```css
.triangle {
  border-width: 100px;
  border-color: #ff00ff transparent transparent transparent;
  border-style: solid dashed dashed dashed;
  width: 0;
  height: 0;
  overflow: hidden;
}

```

如果在less里面匹配的时候，我们没有写top,bottom,left,right,而是瞎写的一个，他只会生成我们的公共样式，
```less
.triangle{
    .sanjiao(fadfadf,100px)
}
```
生成的css
```css
.triangle {
  width: 0;
  height: 0;
  overflow: hidden;
}

```

#### 匹配模式-定位

```less
//匹配模式-定位
.pos(r){
    position:relative;
}
.pos(a){
    position:absolute;
}
.pos(f){
    position:fixed;
}

//使用匹配模式-定位
.div1{
    width:100px;
    height:100px;
    background:#ff0;
    .pos(a);
}
```
生成的css
```css
.div1 {
  width: 100px;
  height: 100px;
  background: #ff0;
  position: absolute;
}

```

#### less里面的运算
任何的数字、颜色、或者变量都可以参与运算、运算应该被包裹在括号中。
例如 +-*/

这里强制规定要不100后面带一个px,要不@test_width后面带一个像素，我们这里@test_width带了一个px，运算符号要前后加空格，否则有的报错，乘除的话，可以使用小括号
less
```less
@test_width:300px;
.box_02{
    width:@test_width + 10;
    height:(@test_width - 50)*2;
    color:#ccc - 20;
}
```
生成的css
css
```css
.box_02 {
  width: 310px;
  height: 500px;
  color: #b8b8b8;
}

```

#### 嵌套规则
- 最有意思的小东西了
- 两种用法
	- &对伪类使用
		- hover或者focus
	- 对连接的使用
		- &-item

html结构
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="style/main.css">
    <title>Document</title>
</head>
<body>
    <ul class="list">
        <li><a href="#">这里是一个测试文字</a><span>2017.6.25</span></li>
        <li><a href="#">这里是一个测试文字</a><span>2017.6.25</span></li>
        <li><a href="#">这里是一个测试文字</a><span>2017.6.25</span></li>
        <li><a href="#">这里是一个测试文字</a><span>2017.6.25</span></li>
        <li><a href="#">这里是一个测试文字</a><span>2017.6.25</span></li>
        <li><a href="#">这里是一个测试文字</a><span>2017.6.25</span></li>
        <li><a href="#">这里是一个测试文字</a><span>2017.6.25</span></li>
        <li><a href="#">这里是一个测试文字</a><span>2017.6.25</span></li>
    </ul>
</body>
</html>
```



less
```less
@charset"utf-8";
//常规写法
// .list{}
// .list li{}
// .list a{}
// .list span{}

//less嵌套写法，注意这里的a是写在list里面还是li里面比较好，我们为了避免让选择器匹配很多次，我们将a与li放到一级
//如果a放在li里面生成css是这样的.list li a{}
//如果让li与a同级，生成的 .list a{} 这样嵌套级数少，效率高
.list{
    width:600px;
    margin:30px auto;
    padding:0;
    list-style: none;

    li{
        height:30px;
        line-height: 30px;
        background:#f00;
        margin-bottom: 5px;

    }
    a{
        float:left;
        //&符号代表他的上一层选择器
        &:hover{
            color:#390;
        }
    }
    span{
        float:right;
    }
}
```
生成的css
```css
@charset "utf-8";
.list {
  width: 600px;
  margin: 30px auto;
  padding: 0;
  list-style: none;
}
.list li {
  height: 30px;
  line-height: 30px;
  background: #f00;
  margin-bottom: 5px;
}
.list a {
  float: left;
}
.list a:hover {
  color: #390;
}
.list span {
  float: right;
}

```


#### arguments变量（用的不是特别多）
- @arguments包含了所有传递进来的参数
- 如果你不想单独处理每个参数的话，就这么写

less
```less
@charset"utf-8";

.border_0(@w:30px,@c:red,@xx:solid){
    border:@w @c @xx;
}
//我懒啊。不想一个个写变量。我们用@arguments全部代替了
.border_1(@w:30px,@c:red,@xx:solid){
    border:@arguments;
}
.div1{
    .border_0(10px);
}
.div2{
    .border_1();
}
```
输出的css
```css
@charset "utf-8";
.div1 {
  border: 10px #ff0000 solid;
}
.div2 {
  border: 30px #ff0000 solid;
}
```

#### 避免编译
- 有的时候我们需要输出一些不正确的css语法或者一些less不认识的专有语法
- 规则是，波浪线加上单引号或者双引号~''
	- 例如 width:~'calc(100%-35)'

```less
@charset"utf-8";
//避免编译，规则为波浪线加单引号或者双引号~""
.test_01{
    width:~'calc(300px-30px)';
}
```
他会原样输出css
```css
@charset "utf-8";
.test_01 {
  width: calc(300px-30px);
}

```

#### !important关键字
会为所有混合所带来的样式，添加上！important
less
```less
@charset"utf-8";
//!important
.border_03(){
    border:solid #080 10px;
}
.test_important{
    .border_03()!important;
}
```

输出的css会自动加上!important
```css
@charset "utf-8";
.test_important {
  border: solid #080 10px !important;
}

```