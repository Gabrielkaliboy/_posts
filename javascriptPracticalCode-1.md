---
title: javascript使用代码段
date: 2017-07-17 15:30:40
categories: 前端
tags: [javascript]
---
<Excerpt in index | 首页摘要> 
javascript使用代码段
<!-- more -->
<The rest of contents | 余下全文>

-----
#### 随机颜色
```html
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
     <button id="btn1">调用第一种</button>
     <button id="bnt2">调用第二种</button>
     <button id="btn3">调用第三种</button>
     <script>
         var btn1=document.getElementById('btn1');
         btn1.onclick=function(){
             document.body.style.background=bg1()
         };
         var btn2=document.getElementById('bnt2');
         btn2.onclick=function(){
             document.body.style.background=bg2();
         };
         var btn3=document.getElementById('btn3');
         btn3.onclick=function(){
             document.body.style.background=bg3();
         };
         function bg1(){
             return '#'+Math.floor(Math.random()*256).toString(10);
         }
         function bg2(){
             return '#'+Math.floor(Math.random()*0xffffff).toString(16);
         }
         function bg3(){
             var r=Math.floor(Math.random()*256);
             var g=Math.floor(Math.random()*256);
             var b=Math.floor(Math.random()*256);
             return "rgb("+r+','+g+','+b+")";//所有方法的拼接都可以用ES6新特性`其他字符串{$变量名}`替换
         }
     </script>
</body>
</html>
```
#### 随机验证码
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<style>
		#code{  
               font-family:Arial;  
               font-style:italic;  
               font-weight:bold;  
               border:0;  
               letter-spacing:2px;  
               color:blue;  
           }
	</style>
	<title>javascript随机验证码</title>
</head>
<body>
	<div>  
	    <input type = "text" id = "input" value="" />  
	    <input type = "button" id="code" onclick="createCode()"/>  
	    <input type = "button" value = "验证" onclick = "validate()"/>  
	</div> 
</body>
<script>
	//设置一个全局的变量，便于保存验证码
	    var code;
	    function createCode(){
	        //首先默认code为空字符串
	        code = '';
	        //设置长度，这里看需求，我这里设置了4
	        var codeLength = 4;
	        var codeV = document.getElementById('code');
	        //设置随机字符
	        var random = new Array(0,1,2,3,4,5,6,7,8,9,'A','B','C','D','E','F','G','H','I','J','K','L','M','N','O','P','Q','R', 'S','T','U','V','W','X','Y','Z');
	        //循环codeLength 我设置的4就是循环4次
	        for(var i = 0; i < codeLength; i++){
	            //设置随机数范围,这设置为0 ~ 36
	             var index = Math.floor(Math.random()*36);
	             //字符串拼接 将每次随机的字符 进行拼接
	             code += random[index]; 
	        }
	        //将拼接好的字符串赋值给展示的Value
	        codeV.value = code;
	    }

	    //下面就是判断是否== 的代码，无需解释
	    function validate(){
	        var oValue = document.getElementById('input').value.toUpperCase();
	        if(oValue ==0){
	            alert('请输入验证码');
	        }else if(oValue != code){
	            alert('验证码不正确，请重新输入');
	            oValue = ' ';
	            createCode();
	        }else{
	            window.open('http://www.baidu.com','_self');
	        }
	    }

	    //设置此处的原因是每次进入界面展示一个随机的验证码，不设置则为空
	    window.onload = function (){

	        createCode();
	    }
</script>
</html>
```