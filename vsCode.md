---
title: vs code使用相关记录
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
![](https://github.com/Gabrielkaliboy/images/blob/master/_posts/vsCode/1.gif?raw=true)

#### Open in Browser
也是用来在浏览器中事先预览的

#### 2.Auto Rename Tag
修改html标签，自动帮你完成尾部闭合标签的同步修改
![](https://github.com/Gabrielkaliboy/images/blob/master/_posts/vsCode/2.gif?raw=true)


#### 3.Auto close Tag
自动闭合标签
![](https://github.com/Gabrielkaliboy/images/blob/master/_posts/vsCode/3.gif?raw=true)

#### 4.Path intellisense
用来路径提示的

####  5.vue的插件vetur
可以轻松在.vue文件里面
- 语法错误检查，包括 CSS/SCSS/LESS/Javascript/TypeScript
- 语法高亮，包括 html/jade/pug css/sass/scss/less/stylus js/ts
- emmet 支持
- 代码自动补全（目前还是初级阶段），包括 HTML/CSS/SCSS/LESS/JavaScript/TypeScript


#### 6.Debugger for Chrome
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

![](https://github.com/Gabrielkaliboy/images/blob/master/_posts/vsCode/4.gif?raw=true)

#### OneDark Pro
说明：用来更改主题的
地址：https://marketplace.visualstudio.com/items?itemName=zhuangtongfa.Material-theme
官网：https://binaryify.github.io/OneDark-Pro/#/
使用说明：Ctrl+k,然后在Ctrl+t
![](https://github.com/Gabrielkaliboy/images/blob/master/_posts/vsCode/5.gif?raw=true)




使用说明
---
#### 移除当前文件目录
文件--->关闭文件夹


vs code+xampp+php搭建php开发调试环境
---
#### 1.安装php-debug
打开vs code直接快捷键Ctrl+p,输入`ext install php-debug` 安装调试插件 

#### 2.下载xdebug
去 https://xdebug.org/download.php 下载php对应版本的插件，php版本可以在xampp中的readme看到，下载这个PHP 5.6 VC11 TS (32 bit) 把dll文件拷贝到php(xampp文件目录下面的php文件夹)目录
![](https://github.com/Gabrielkaliboy/images/blob/master/_posts/vsCode/1.png?raw=true)

#### 3.配置php.ini
在xampp安装目录的php文件夹下面找到php.ini,加入如下代码,其中zend_extension的路径改为我们正确的位置，配置完成后重启apache服务器
```
zend_extension=D:\xampp\php\php_xdebug-2.5.5-7.0-vc14.dll
[XDebug]
xdebug.remote_enable = 1
xdebug.remote_autostart = 1
``` 
#### 4.第一次安装vs会提示这个，需要配置下php.exe的路径，在用户设置里添加以下项
![](https://github.com/Gabrielkaliboy/images/blob/master/_posts/vsCode/2.png?raw=true)

打开文件--->首选项---->设置，填入真是的php.exe路径

![](https://github.com/Gabrielkaliboy/images/blob/master/_posts/vsCode/3.png?raw=true)

#### 5.在vscode中的php文件打一断点，点Listen for XDebug 项目的运行，配置不用更改，默认就可以
![](https://github.com/Gabrielkaliboy/images/blob/master/_posts/vsCode/4.png?raw=true) 

#### 6.php文件要做xampp对应的目录下，直接在浏览器运行，注意是服务器地址，然后打断点就可以调试了
直接在浏览器中打开要调试的php（不是文件路径而是服务器的地址(http://127.0.0.1/test.php)）,vscode就会命中到打断点的地方


#### 注意
php最大执行时间好像是30秒，超过30秒会自动终止，因此调试的时候要修改一下时间，在php.ini 文件中修改最大运行时间为5分钟
```
max_execution_time=3000
```

vs code 编写markdown文件
---
#### 1. vs code 与markdown
vs code最新版本已经默认支持markdown

#### Auto-Open Markdown Preview
说明：实时预览插件
网址：https://marketplace.visualstudio.com/items?itemName=hnw.vscode-auto-open-markdown-preview
安装代码：ext install vscode-auto-open-markdown-preview

vs code里面使用git
---
#### 1.参考
http://www.cnblogs.com/xuanhun/p/6019038.html?utm_source=tuicool&utm_medium=referral