---
title: jQuery validate 使用说明
date: 2017-06-12 19:01:40
categories: 前端
tags: [前端开发插件]
---
<Excerpt in index | 首页摘要> 
jQuery validate 使用说明
<!-- more -->
<The rest of contents | 余下全文>

-----
#### 1.介绍
jQuery validate是一款专门用来做表单验证的插件，该插件是由 Jörn Zaefferer 编写和维护的，他是 jQuery 团队的一名成员，是 jQuery UI 团队的主要开发人员，是 QUnit 的维护人员。该插件在 2006 年 jQuery 早期的时候就已经开始出现，并一直更新至今。目前版本是 1.14.0。

官网：https://jqueryvalidation.org/
GitHub：https://github.com/jquery-validation/jquery-validation
菜鸟：http://www.runoob.com/jquery/jquery-plugin-validate.html

#### 2.使用方法（详细的见上面的菜鸟链接）
##### 2.1引入必要的文件
- 引入jQuery
- 引入validate.min.js
- 菜鸟cdn
	```javascript
	<script src="http://static.runoob.com/assets/jquery-validation-1.14.0/lib/jquery.js"></script>
	<script src="http://static.runoob.com/assets/jquery-validation-1.14.0/dist/jquery.validate.min.js"></script>
	```

##### 2.2默认校验规则
<table class="reference">
<tbody><tr>
	<th width="10%">序号</th>
	<th width="30%">规则</th>
    <th width="60%">描述</th>
</tr>
<tr>
	<td>1</td>
    <td>required:true</td>
	<td>必须输入的字段。</td>
</tr>
<tr>
	<td>2</td>
    <td>remote:"check.php"</td>
	<td>使用 ajax 方法调用 check.php 验证输入值。</td>
</tr>
<tr>
	<td>3</td>
    <td>email:true</td>
	<td>必须输入正确格式的电子邮件。</td>
</tr>
<tr>
	<td>4</td>
    <td>url:true</td>
	<td>必须输入正确格式的网址。</td>
</tr>
<tr>
	<td>5</td>
    <td>date:true</td>
	<td>必须输入正确格式的日期。日期校验 ie6 出错，慎用。</td>
</tr>
<tr>
	<td>6</td>
    <td>dateISO:true</td>
	<td>必须输入正确格式的日期（ISO），例如：2009-06-23，1998/01/22。只验证格式，不验证有效性。</td>
</tr>
<tr>
	<td>7</td>
    <td>number:true</td>
	<td>必须输入合法的数字（负数，小数）。</td>
</tr>
<tr>
	<td>8</td>
    <td>digits:true</td>
	<td>必须输入整数。</td>
</tr>
<tr>
	<td>9</td>
    <td>creditcard:</td>
	<td>必须输入合法的信用卡号。</td>
</tr>
<tr>
	<td>10</td>
    <td>equalTo:"#field"</td>
	<td>输入值必须和 #field 相同。</td>
</tr>
<tr>
	<td>11</td>
    <td>accept:</td>
	<td>输入拥有合法后缀名的字符串（上传文件的后缀）。</td>
</tr>
<tr>
	<td>12</td>
    <td>maxlength:5</td>
	<td>输入长度最多是 5 的字符串（汉字算一个字符）。</td>
</tr>
<tr>
	<td>13</td>
    <td>minlength:10</td>
	<td>输入长度最小是 10 的字符串（汉字算一个字符）。</td>
</tr>
<tr>
	<td>14</td>
    <td>rangelength:[5,10]</td>
	<td>输入长度必须介于 5 和 10 之间的字符串（汉字算一个字符）。</td>
</tr>
<tr>
	<td>15</td>
    <td>range:[5,10]</td>
	<td>输入值必须介于 5 和 10 之间。</td>
</tr>
<tr>
	<td>16</td>
    <td>max:5</td>
	<td>输入值不能大于 5。</td>
</tr>
<tr>
	<td>17</td>
    <td>min:10</td>
	<td>输入值不能小于 10。</td>
</tr>
</tbody></table>


#### 3.一个完整的注册示例（没有验证码）
GitHub地址：https://github.com/Gabrielkaliboy/markdown/tree/master/demo/jQuery-validate/register

![](jQueryValidate/1.gif);

#### 4.分步校验(版权所有，转载注明出处)
GitHub地址：

![](jQueryValidate/2.gif);

#### 5.注意事项
##### 5.1关于select的required校验问题
只要select里面的第一个option没有value值，就可以进行校验，应为这时候value是空，用户相当于没有输入
```html
<select name="detailBusiness" id="detailBusiness">
    <option value="">选择行业</option>
    <option value="1">计算机硬件及网络设备</option>
    <option value="2">计算机软件</option>
    <option value="3">IT服务（系统/数据/维护）</option>
    <option value="4">互联网/电子商务</option>
    <option value="5">通讯（设备/运营/增资服务）</option>
    <option value="6">电子技术/半导体/集成电路</option>
<select>
```
##### 5.2radio 和 checkbox、select 的验证
建议查看http://www.runoob.com/jquery/jquery-plugin-validate.html