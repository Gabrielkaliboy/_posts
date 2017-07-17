---
title:vs code使用相关记录
date: 2017-06-19 09:09:40
categories: 软件
tags: [前端,javascript,vue]
---
<Excerpt in index | 首页摘要> 
vsCode
<!-- more -->
<The rest of contents | 余下全文>

-----

### 插件
---
在vs里面使用快捷键Ctrl+p来安装插件

#### 1.View In Browser
用来在vs code里面预览html文件，默认的快捷键Ctrl+F1
注：只支持html文件
![](vsCode/1.gif)

#### Open in Browser
也是用来在浏览器中事先预览的

#### 2.Auto Rename Tag
修改html标签，自动帮你完成尾部闭合标签的同步修改
![](vsCode/2.gif)


#### 3.Auto close Tag
自动闭合标签
![](vsCode/3.gif)

#### 4.Path intellisense
用来路径提示的

####  5.vue的插件vetur
可以轻松在.vue文件里面
- 语法错误检查，包括 CSS/SCSS/LESS/Javascript/TypeScript
- 语法高亮，包括 html/jade/pug css/sass/scss/less/stylus js/ts
- emmet 支持
- 代码自动补全（目前还是初级阶段），包括 HTML/CSS/SCSS/LESS/JavaScript/TypeScript


#### Debugger for Chrome
- 下载地址：https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome
- 说明：可以在vs里面直接用Chrome进行调试
- 环境搭建
	- 安装完了插件以后，在调试界面添加Chrome环境，然后在打开的launch.json里面写入配置，
	- 默认launch.json里面是这样的
	```
	{
	    "version": "0.2.0",
	    "configurations": [
	        
	        {
	            "type": "chrome",
	            "request": "launch",
	            "name": "Launch Chrome against localhost",
	            "url": "http://localhost:8080",
	            "webRoot": "${workspaceRoot}"
	        },
	        {
	            "type": "chrome",
	            "request": "attach",
	            "name": "Attach to Chrome",
	            "port": 9222,
	            "webRoot": "${workspaceRoot}"
	        }
	    ]
	}
	```
	- 更改以后是这样的

	```
	{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Launch index.html (disable sourcemaps)",//就是这个
            "type": "chrome",
            "request": "launch",
            "sourceMaps": false,
            "file": "${workspaceRoot}/index.html"//你的文件名字叫什么，这里就写什么，或者不写，直接到的是文件夹目录
        },       
        {
            "type": "chrome",
            "request": "launch",
            "name": "Launch Chrome against localhost",
            "url": "http://localhost:8080",
            "webRoot": "${workspaceRoot}"
        },
        {
            "type": "chrome",
            "request": "attach",
            "name": "Attach to Chrome",
            "port": 9222,
            "webRoot": "${workspaceRoot}"
        }
	    ]
	}
	```
	- 将配置文件改好了以后，就可以使用了，记得调试的时候选择我们刚才改的那个

![](vsCode/4.gif)

### 使用说明

#### 移除当前文件目录
文件--->关闭文件夹
