---
title: 前端开发过程中的bug以及兼容性记录（一）
date: 2017-06-27 18:00:40
categories: 前端
tags: [bug记录]
---
<Excerpt in index | 首页摘要> 
前端开发过程中的bug以及兼容性记录（一）
<!-- more -->
<The rest of contents | 余下全文>

-----

#### 1.IE浏览器文件上传返回的json会提示你下载
如图
![](bugCompatibility/1.png)

解决方式：
根据不同的后台语言进行搜索搜索，关键字
- IE 文件上传返回json
- .net上传返回json

修改一下后台返回的数据类型就可以
