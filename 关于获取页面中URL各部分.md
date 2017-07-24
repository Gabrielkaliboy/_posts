---
title: 关于获取页面中URL各部分
date: 2017-06-06 22:46:39
categories: 前端
tags: [javascript,html]
---
<Excerpt in index | 首页摘要> 
关于获取页面中URL各部分
<!-- more -->
<The rest of contents | 余下全文>
---
# 其实就是与window.location后面的属性有关
window.location

属性                  描述

hash                设置或获取 href 属性中在井号“#”后面的分段。

host                 设置或获取 location 或 URL 的 hostname 和 port 号码。

hostname      设置或获取 location 或 URL 的主机名称部分。

href                  设置或获取整个 URL 为字符串。

pathname      设置或获取对象指定的文件名或路径。

port                  设置或获取与 URL 关联的端口号码。

protocol          设置或获取 URL 的协议部分。

search            设置或获取 href 属性中跟在问号后面的部分。
### 设置或获取对象指定的文件名或路径
语法：window.location.pathname

例如:`http://localhost:1567/documentCenter?2#DeviceCalibrateView`

输出`"/documentCenter"`

### 设置或获取整个 URL 为字符串
语法：window.location.href

例如:`http://localhost:1567/documentCenter?2#DeviceCalibrateView`

输出：`"http://localhost:1567/documentCenter?2#DeviceCalibrateView"`

### 设置或获取与 URL 关联的端口号码
语法：window.location.port

例如:`http://localhost:1567/documentCenter?2#DeviceCalibrateView`

输出：`"1567"`

### 设置或获取 URL 的协议部分
语法：window.location.protocol

例如:`http://localhost:1567/documentCenter?2#DeviceCalibrateView`

输出：`"http:"`

### 设置或获取 href 属性中在井号“#”后面的分段
语法：window.location.hash

例如:`http://localhost:1567/documentCenter?2#DeviceCalibrateView`

输出：`"#DeviceCalibrateView"`

### 设置或获取 location 或 URL 的 hostname 和 port 号码
语法：window.location.host

例如:`http://localhost:1567/documentCenter?2#DeviceCalibrateView`

输出：`"localhost:1567"`

### 设置或获取 href 属性中跟在问号后面的部分
语法：window.location.search

例如:`http://localhost:1567/documentCenter?2#DeviceCalibrateView`

输出：`"?2"`

附上一个关于PHP中服务器变量获取query字符串的各个参数方法：[点我](http://blog.unvs.cn/archives/php-server-url-string.html)

页面中不使用window对象获取，参考javascript实用代码块=部分：[点我](https://github.com/Gabrielkaliboy/javascriptPracticalCode/blob/master/javascriptPracticalCode_1.md)


