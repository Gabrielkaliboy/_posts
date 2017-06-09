---
title: jQueryDatatables1.10.0使用说明
date: 2017-06-08 11:02:40
categories: 前端
tags: [jQuery,前端开发插件,javascript]
---
<Excerpt in index | 首页摘要> 
<!-- more -->
<The rest of contents | 余下全文>

-----
#### 1. 介绍
Datatables是一款jquery表格插件。它是一个高度灵活的工具，可以将任何HTML表格添加高级的交互功能。
- 分页，即时搜索和排序
- 几乎支持任何数据源：DOM， javascript， Ajax 和 服务器处理
- 支持不同主题 DataTables, jQuery UI, Bootstrap, Foundation
- 各式各样的扩展: Editor, TableTools, FixedColumns ……
- 丰富多样的option和强大的API
- 支持国际化
- 超过2900+个单元测试
- 免费开源 （ MIT license ）！ 商业支持
- 更多特性请到官网查看

官网：https://www.datatables.net/
英文官网GitHub：https://github.com/DataTables/DataTables
中文网：http://www.datatables.club/
中文网GitHub：https://github.com/ssy341/datatables-cn

**特别说明：**实际项目开发中使用的是1.10.0版本，写这个总结的时候，官网已经更新到了1.10.15

#### 2. 使用方法
基于jQuery的，所以首先需要引入jQuery，然后在引入datatable的js和css
```html
<script src="https://cdn.bootcss.com/jquery/1.10.2/jquery.js"></script>
<script type="text/javascript" src="jquery.dataTables.min.js"></script>
<link rel="stylesheet" href="https://cdn.datatables.net/1.10.15/css/jquery.dataTables.min.css" >
```
一个简单的demo1.html,注意涉及到ajax请求，涉及到同源策略了，所以要在本地服务器上跑,效果如图：
![](jQueryDataTables1.10.0/1.gif)
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<script src="https://cdn.bootcss.com/jquery/1.10.2/jquery.js"></script>
	<script type="text/javascript" src="jquery.dataTables.min.js"></script>
	<link rel="stylesheet" href="https://cdn.datatables.net/1.10.15/css/jquery.dataTables.min.css" >
	<style>
		.main{
			width:1100px;
			margin:100px auto;
		}
		td{
			text-align: center;
		}
	</style>
	<title></title>
</head>
<body>
	<div class="main">
		<table cellpadding="0" cellspacing="0" id="example">
			<thead>
			  <tr>
			    <th>Rendering engine</th>
			    <th>Browser</th>
			    <th>Platform(s)</th>
			    <th>Engine version</th>
			    <th>CSS grade</th>
			  </tr>
			</thead>
		    <tbody></tbody>
		</table>
	</div>
</body>
<script type="text/javascript">
	$(document).ready(function() {
		$('#example').dataTable( {
			"bProcessing": true,//当datatable获取数据时候是否显示正在处理提示信息。
			"sAjaxSource": 'arrays.txt'//指定要从哪个URL获取数据
		} );
	} );
</script>
</html>
```
arrays.txt文件
```txt
{
  "aaData": [
    [
      "Trident",
      "Internet Explorer 4.0",
      "Win 95+",
      "4",
      "X"
    ],
    [
      "Trident",
      "Internet Explorer 5.0",
      "Win 95+",
      "5",
      "C"
    ],
    [
      "Trident",
      "Internet Explorer 5.5",
      "Win 95+",
      "5.5",
      "A"
    ],
    [
      "Trident",
      "Internet Explorer 6",
      "Win 98+",
      "6",
      "A"
    ],
    [
      "Trident",
      "Internet Explorer 7",
      "Win XP SP2+",
      "7",
      "A"
    ],
    [
      "Trident",
      "AOL browser (AOL desktop)",
      "Win XP",
      "6",
      "A"
    ],
    [
      "Gecko",
      "Firefox 1.0",
      "Win 98+ / OSX.2+",
      "1.7",
      "A"
    ],
    [
      "Gecko",
      "Firefox 1.5",
      "Win 98+ / OSX.2+",
      "1.8",
      "A"
    ],
    [
      "Gecko",
      "Firefox 2.0",
      "Win 98+ / OSX.2+",
      "1.8",
      "A"
    ],
    [
      "Gecko",
      "Firefox 3.0",
      "Win 2k+ / OSX.3+",
      "1.9",
      "A"
    ],
    [
      "Gecko",
      "Camino 1.0",
      "OSX.2+",
      "1.8",
      "A"
    ],
    [
      "Gecko",
      "Camino 1.5",
      "OSX.3+",
      "1.8",
      "A"
    ],
    [
      "Gecko",
      "Netscape 7.2",
      "Win 95+ / Mac OS 8.6-9.2",
      "1.7",
      "A"
    ],
    [
      "Gecko",
      "Netscape Browser 8",
      "Win 98SE+",
      "1.7",
      "A"
    ],
    [
      "Gecko",
      "Netscape Navigator 9",
      "Win 98+ / OSX.2+",
      "1.8",
      "A"
    ],
    [
      "Gecko",
      "Mozilla 1.0",
      "Win 95+ / OSX.1+",
      1,
      "A"
    ],
    [
      "Gecko",
      "Mozilla 1.1",
      "Win 95+ / OSX.1+",
      1.1,
      "A"
    ],
    [
      "Gecko",
      "Mozilla 1.2",
      "Win 95+ / OSX.1+",
      1.2,
      "A"
    ],
    [
      "Gecko",
      "Mozilla 1.3",
      "Win 95+ / OSX.1+",
      1.3,
      "A"
    ],
    [
      "Gecko",
      "Mozilla 1.4",
      "Win 95+ / OSX.1+",
      1.4,
      "A"
    ],
    [
      "Gecko",
      "Mozilla 1.5",
      "Win 95+ / OSX.1+",
      1.5,
      "A"
    ],
    [
      "Gecko",
      "Mozilla 1.6",
      "Win 95+ / OSX.1+",
      1.6,
      "A"
    ],
    [
      "Gecko",
      "Mozilla 1.7",
      "Win 98+ / OSX.1+",
      1.7,
      "A"
    ],
    [
      "Gecko",
      "Mozilla 1.8",
      "Win 98+ / OSX.1+",
      1.8,
      "A"
    ],
    [
      "Gecko",
      "Seamonkey 1.1",
      "Win 98+ / OSX.2+",
      "1.8",
      "A"
    ],
    [
      "Gecko",
      "Epiphany 2.20",
      "Gnome",
      "1.8",
      "A"
    ],
    [
      "Webkit",
      "Safari 1.2",
      "OSX.3",
      "125.5",
      "A"
    ],
    [
      "Webkit",
      "Safari 1.3",
      "OSX.3",
      "312.8",
      "A"
    ],
    [
      "Webkit",
      "Safari 2.0",
      "OSX.4+",
      "419.3",
      "A"
    ],
    [
      "Webkit",
      "Safari 3.0",
      "OSX.4+",
      "522.1",
      "A"
    ],
    [
      "Webkit",
      "OmniWeb 5.5",
      "OSX.4+",
      "420",
      "A"
    ],
    [
      "Webkit",
      "iPod Touch / iPhone",
      "iPod",
      "420.1",
      "A"
    ],
    [
      "Webkit",
      "S60",
      "S60",
      "413",
      "A"
    ],
    [
      "Presto",
      "Opera 7.0",
      "Win 95+ / OSX.1+",
      "-",
      "A"
    ],
    [
      "Presto",
      "Opera 7.5",
      "Win 95+ / OSX.2+",
      "-",
      "A"
    ],
    [
      "Presto",
      "Opera 8.0",
      "Win 95+ / OSX.2+",
      "-",
      "A"
    ],
    [
      "Presto",
      "Opera 8.5",
      "Win 95+ / OSX.2+",
      "-",
      "A"
    ],
    [
      "Presto",
      "Opera 9.0",
      "Win 95+ / OSX.3+",
      "-",
      "A"
    ],
    [
      "Presto",
      "Opera 9.2",
      "Win 88+ / OSX.3+",
      "-",
      "A"
    ],
    [
      "Presto",
      "Opera 9.5",
      "Win 88+ / OSX.3+",
      "-",
      "A"
    ],
    [
      "Presto",
      "Opera for Wii",
      "Wii",
      "-",
      "A"
    ],
    [
      "Presto",
      "Nokia N800",
      "N800",
      "-",
      "A"
    ],
    [
      "Presto",
      "Nintendo DS browser",
      "Nintendo DS",
      "8.5",
      "C/A<sup>1</sup>"
    ],
    [
      "KHTML",
      "Konqureror 3.1",
      "KDE 3.1",
      "3.1",
      "C"
    ],
    [
      "KHTML",
      "Konqureror 3.3",
      "KDE 3.3",
      "3.3",
      "A"
    ],
    [
      "KHTML",
      "Konqureror 3.5",
      "KDE 3.5",
      "3.5",
      "A"
    ],
    [
      "Tasman",
      "Internet Explorer 4.5",
      "Mac OS 8-9",
      "-",
      "X"
    ],
    [
      "Tasman",
      "Internet Explorer 5.1",
      "Mac OS 7.6-9",
      "1",
      "C"
    ],
    [
      "Tasman",
      "Internet Explorer 5.2",
      "Mac OS 8-X",
      "1",
      "C"
    ],
    [
      "Misc",
      "NetFront 3.1",
      "Embedded devices",
      "-",
      "C"
    ],
    [
      "Misc",
      "NetFront 3.4",
      "Embedded devices",
      "-",
      "A"
    ],
    [
      "Misc",
      "Dillo 0.8",
      "Embedded devices",
      "-",
      "X"
    ],
    [
      "Misc",
      "Links",
      "Text only",
      "-",
      "X"
    ],
    [
      "Misc",
      "Lynx",
      "Text only",
      "-",
      "X"
    ],
    [
      "Misc",
      "IE Mobile",
      "Windows Mobile 6",
      "-",
      "C"
    ],
    [
      "Misc",
      "PSP browser",
      "PSP",
      "-",
      "C"
    ],
    [
      "Other browsers",
      "All others",
      "-",
      "-",
      "U"
    ]
  ]
}
```
#### 3. 部分API

使用的时候，部分属性
<table border="1" cellspacing="0" cellpadding="0" style="line-height:26px; font-family:Arial; color:rgb(51,51,51); font-size:14px">
<tbody>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">属性名称</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">取值局限</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">申明</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">bAutoWidth</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">true or false， default true</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">是否主动策画表格各列宽度</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">bDeferRender</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">true or false， default false</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">用于衬着的一个参数</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">bFilter</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">true or false， default true</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">开关，是否启用客户端过滤功能</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">bInfo</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">true or false， default true</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">开关，是否显示表格的一些信息</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">bJQueryUI</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">true or false， default false</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">是否应用jquery ui themeroller的风格</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">bLengthChange</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">true or false， default true</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">开关，是否显示一个每页长度的选择条（须要分页器支撑）</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">bPaginate</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">true or false， default true</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">开关，是否显示（应用）分页器</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">bProcessing</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">true or false， defualt false</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">当datatable获取数据时候是否显示正在处理提示信息。</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">bScrollInfinite</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">true or false， default false</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">开关，以指定是否无穷迁移转变（与sScrollY共同应用），在<a href="http://lib.csdn.net/base/hadoop" class="replace_word" title="Hadoop知识库" target="_blank" style="color:#df3434; font-weight:bold;">大数据</a>量的时辰很有效。当这个标记为true的时辰，分页器就默认封闭</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">bSort</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">true or false， default true</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">开关，是否让各列具有按列排序功能</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">bSortClasses</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">true or false， default true</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">开关，指定当当前列在排序时，是否增长classes ""sorting_1""， ""sorting_2"" and ""sorting_3""，打开后，在处理惩罚大数据时，机能有所丧失</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">bStateSave</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">true or false， default false</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">开关，是否打开客户端状况记录功能。这个数据是记录在cookies中的，打开了这个记录后，即使刷新一次页面，或从头打开浏览器，之前的状况都是保存下来的</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">sScrollX</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">""disabled"" or? ""100％""?类似的字符串</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">是否开启程度迁移转变，以及指定迁移转变区域大小</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">sScrollY</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">""disabled"" or ""200px""?类似的字符串</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">是否开启垂直迁移转变，以及指定迁移转变区域大小</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">--</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">--</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">--</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">选项</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">?</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">?</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">aaSorting</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">array array[int，string]，如[]， [[0，""asc""]， [0，""desc""]]</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">指定按多列数据排序的根据</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">aaSortingFixed</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">同上</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">同上。独一不合点是不克不及被用户的自定义设备冲突</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">aLengthMenu</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">default [10， 25， 50， 100]，可认为一维数组，也可为二维数组，比如：[[10， 25， 50， -1]， [10， 25， 50， "All"]]</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">这个为选择每页的条目数，当应用一个二维数组时，二维层面只能有两个元素，第一个为显示每页条目数的选项，第二个是关于这些选项的申明</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">aoSearchCols</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">default null，?类似：[null， {"sSearch": "My filter"}， null，{"sSearch": "^[0-9]"， "bEscapeRegex": false}]</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">给每个列零丁定义其初始化搜刮列表特点（这一块还没搞懂）</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">asStripClasses</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">default [""odd""， ""even""]，?比如[""strip1""， ""strip2""， ""strip3""]</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">指定要被应用到各行的class风格，会主动轮回</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">bDestroy</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">true or false， default false</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">用于当要在同一个元素上履行新的dataTable绑按时，将之前的那个数据对象清除掉，换以新的对象设置</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">bRetrieve</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">true or false， default false</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">用于指明当履行dataTable绑按时，是否返回DataTable对象</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">bScrollCollapse</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">true or false， default false</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">指定恰当的时辰缩起迁移转变视图</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">bSortCellsTop</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">true or false， default false</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">（未知的东东）</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">iCookieDuration</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">整数，默认7200，单位为秒</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">指定用于存储客户端信息到cookie中的时候长度，跨越这个时候后，主动过期</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">iDeferLoading</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">整数，默认为null</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">延迟加载，它的参数为要加载条目标数量，凡是与bServerSide，sAjaxSource等共同应用</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">iDisplayLength</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">整数，默认为10</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">用于指定一屏显示的条数，需开启分页器</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">iDisplayStart</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">整数，默认为0</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">用于指定从哪一条数据开端显示到表格中去</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">iScrollLoadGap</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">整数，默认为100</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">用于指定当DataTable设置为迁移转变时，最多可以一屏显示几许条数据</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">oSearch</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">默认{ "sSearch": ""， "bRegex": false， "bSmart": true }</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">又是初始时指定搜刮参数相干的，有点错杂，没搞懂今朝</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">sAjaxDataProp</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">字符串，default ""aaData""</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">指定当从办事端获取表格数据时，数据项应用的名字</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">sAjaxSource</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">URL字符串，default null</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">指定要从哪个URL获取数据</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">sCookiePrefix</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">字符串，default ""SpryMedia_DataTables_""</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">当打开状况存储特点后，用于指定存储在cookies中的字符串的前缀名字</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">sDom</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">default lfrtip （when bJQueryUI is false） or &lt;"H"lfr&gt;t&lt;"F"ip&gt; （when bJQueryUI is true）</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">这是用于定义DataTable布局的一个强大的属性，另开专门文档来补充申明吧</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">sPaginationType</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">""full_numbers"" or ""two_button""， default ""two_button""</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">用于指定分页器风格</span></p>
</td>
</tr>
<tr>
<td valign="top">
<p align="left"><span style="font-size:10px">sScrollXInner</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">string default ""disabled""</span></p>
</td>
<td valign="top">
<p align="left"><span style="font-size:10px">又是程度迁移转变相干的，没搞懂啥意思</span></p>
<div><span style="font-size:10px"><br>
</span></div>
</td>
</tr>
</tbody>
</table>

#### 4.一个复杂的例子