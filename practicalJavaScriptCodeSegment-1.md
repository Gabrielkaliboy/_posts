---
title: 超实用的javascript代码段
date: 2017-06-13 17:01:40
categories: 前端
tags: [javascript,实用代码段]
---
<Excerpt in index | 首页摘要> 
超实用的javascript代码段
<!-- more -->
<The rest of contents | 余下全文>

-----
#### 1.禁止表单按回车触发提交事件
在HTML页里面由于使用了form，常常需要禁用enter提交表单。因为内容页或者母版页自身有如果有type="submit"的button,当textbox聚焦时，按下enter都会触发表单的默认提交（不论是IE还是firefox），于是需要在onkeydown中监听用户的按键。实际测试，IE8中导致表单提交的不确定因素太多，点击表单的table中的td都会触发表单提交，而firefox则不会；于是在ie和ff中禁用表单提交需要不同的思路。

- 对于IE:
只有当事件源是TEXTAREA时才return true，允许默认动作；其他元素全部return false，禁止表单提交和任何响应。

- 对于firefox:
只有当事件源是INPUT时才return false禁止表单默认动作；而其他元素则return true允许默认动作，比如textarea的多行输入。

代码段
```javascript
//禁用Enter键表单自动提交    
document.onkeydown = function(event) {    
   var target, code, tag;    
   if (!event) {    
       event = window.event; //针对ie浏览器    
       target = event.srcElement;    
       code = event.keyCode;    
       if (code == 13) {    
           tag = target.tagName;  
           //判断是不是textarea，如果是返回true，不是则禁用  
           if (tag == "TEXTAREA") { return true; }    
           else { return false; }    
       }    
   }    
   else {    
       target = event.target; //针对遵循w3c标准的浏览器，如Firefox    
       code = event.keyCode;    
       if (code == 13) {    
           tag = target.tagName;    
           if (tag == "INPUT") { return false; }    
           else { return true; }    
       }    
   }    
};  
```