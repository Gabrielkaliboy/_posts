---
title: javascript数学函数
date: 2017-07-11 19:15:40
categories: 前端
tags: [javascript]
---
<Excerpt in index | 首页摘要> 
javascript数学函数
<!-- more -->
<The rest of contents | 余下全文>
### js中关于Math函数的详细文档：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/asin


### 1.绝对值
语法：`Math.abs()`
eg:
```
Math.abs(-9);
//返回9
```

### 2.大于等会x的最小整数（上取整）
语法：Math.ceil(x);
eg:
```
Math.ceil(1.2);
//返回2
Math.ceil(1.6);
//返回2
```

### 3.小于等于x的最大整数（下取整）
语法：Math.floor(x);
eg:
```
Math.floor(2.9);
//2
Math.floor(2.1);
//2
```

### 4.返回一个0-1之间的随机数
语法：Math.random
eg:
```
Math.random()
//0.14841932773092714
Math.random()
//0.46448853815957114
Math.random()
//0.012237218272461492
```
### 5.π
语法：Math.PI
eg:
```
Math.PI
//3.141592653589793
```
### 可能会用到
![](https://github.com/Gabrielkaliboy/markdown/blob/master/images/images/triangle.jpg?raw=true)

### 6.正玄
语法：Math.sin(x);
注意：这里的x如果只是传入1,2,3这样的数字，他代表的可能是弧度（未验证），反正Math.sin(30)不等于0.5，需要与5合起来用。
eg:
```
Math.sin(30);
//-0.9880316240928618
Math.sin(Math.PI/6);
//0.49999999999999994
```

### 7.余弦
语法：Math.cos(x)
eg:
```
Math.cos(Math.PI/3);
//0.5
```
### 8.正切
语法：Math.tan(x);
eg:
```
Math.tan(Math.PI/4)
//0.9999999999999999
```
### 9.反余弦
语法：Math.acos(x);
注意：x是介于-1.0-1.0之间，如果超出这个范围，浏览器返回NaN,且返回的是0-π之间的弧度值，要是想使用度，还得转一下
eg:
```
Math.acos(0.5)
//1.0471975511965979

Math.acos(0.5)*(180/Math.PI)
//60.00000000000001
```
### 10.反正弦
语法：Math.asin(x);
注意：返回的值是 -PI/2 到 PI/2 之间的弧度值
eg:
```
Math.asin(0.5)
//0.5235987755982989
Math.asin(0.5)*(180/Math.PI)
//30.000000000000004
```

### 11.反正切
语法：Math.atan(x)
eg:
```
Math.atan(1)
//0.7853981633974483
Math.atan(1)*(180/Math.PI)
//45
```

### 12.返回一堆数中较大的那个
语法：Math.max(a,b,c,d,e,f....)
eg:
```
Math.max(8,8,12,47,65,18)
//65
Math.max(8)
//8
Math.max(8,8)
//8
```

### 13.返回一组数中最小的那个
语法：Math.min(a,b,c,d,e,f,g);
eg:
```
Math.min(1,5,8,74,32,0,9,41)
//0
Math.min(1,5)
//1
Math.min(5,5)
//5
```

### 14.x的y次幂（x的y次方）
语法：Math.pow(x,y);
eg:
```
Math.pow(2,3)
//8
Math.pow(1,3)
//1
Math.pow(4,0)
//1
```

### 15.返回数的平方根
语法：Math.sqrt(x);
注意：x不能为负数，否则返回NaN
eg:
```
Math.sqrt(4)
//2
Math.sqrt(0)
//0
Math.sqrt(-9)
//NaN
```

### 16.四舍五入取整
语法：Math.round(x);
eg:
```
Math.round(2.1)
//2
Math.round(2.5)
//3
```

### 17.设置数字固定长度
语法：toPrecision(x),x为指定的数字长度
注意：他的返回值是string类型
eg:
```
10.0000.toPrecision(2)
//"10"
10.0000.toPrecision(3)
//"10.0"
10.0000.toPrecision(6)
//"10.0000"
10.0000.toPrecision(8)
//"10.000000"
var x=3.23.toPrecision(1)
//undefined
x
//"3"
typeof x
//"string"
```

### 18.保留几位小数
语法：toFixed(x),x为指定保留几位小数
注意：他的返回值是number类型
eg:
```
0.4586254.toFixed(2)
//"0.46"
0.4586254.toFixed(3)
//"0.459"
var x=0.1248721;
//undefined
x.toFixed(3)
//"0.125"
typeof x
//"number"
```

### 19.parseFloat(x)
- 用来解析一个字符串的,返回数字,x是一个字符串
```
parseFloat("10")
//10
```
- 自动忽略两边空格
```
parseFloat("    10  ")
//10
```
- 如果数与数之间出现空格，也会停止
```
parseFloat("10 15 14")
//10
```
- 首个字符如果不是数字，则返回NaN
```
parseFloat("d10")
//NaN
```
- 向后遇到非数字会停止，并将非数字之前的字符串转为数字并返回,比如下面字符串中的b
```
parseFloat("    10df54")
10
```

- 如果在解析过程中遇到了正负号（+ 或 -）、数字 (0-9)、小数点，或者科学记数法中的指数（e 或 E）以外的字符，则它会忽略该字符以及之后的所有字符，返回当前已经解析到的浮点数
```
parseFloat("-10")
//-10
parseFloat("-10.8")
//-10.8
parseFloat("e")
//NaN
parseFloat("10-8")
//10
```

### 20.parseInt(string, radix)
- 说明：用来解析一个字符串并返回整数
- radix:可选。表示要解析的数字的基数。该值介于 2 ~ 36 之间。如果省略该参数或其值为 0，则数字将以 10 为基础来解析。如果它以 “0x” 或 “0X” 开头，将以 16 为基数。如果该参数小于 2 或者大于 36，则 parseInt() 将返回 NaN。

- 如果开头是字母，会返回NaN
```
parseInt("adf")
//NaN
```

- 只有字符串中的第一个数字会被返回
```
parseInt("78cd65")
//78

parseInt("78  65")
//78
```

- 开头结尾允许有空格
```
parseInt("  78  ")
//78
```

- 给定参数radix为16，代表16进制
```
parseInt("  1a  ",16)
//26
//就是16+10=26
```

- 如果 string 以 "0x" 开头，parseInt() 会把 string 的其余部分解析为十六进制的整数
```
parseInt("0x11")
//17
```

- 如果 string 以 1 ~ 9 的数字开头，parseInt() 将把它解析为十进制的整数。(ES5)
```
parseInt("04")
//4
```

### 21.判断数据是字符串还是数字
语法：isNaN(x)
说明：如果是字符串，isNaN返回true，如果是数字，isNaN则返回false。
注意：数字两边加双引号的情况
```
isNaN("adf")
//true
isNaN("1415")
//false
isNaN(1117)
//false
isNaN("455dc")
//true
```

### 22.求余数
语法：x%y
说明：x除以y的余数
eg:
```
1%0.3
//0.10000000000000003

9%2
//1
10%2
//0
```
### 23.Math.SQRT1_2
说明：返回返回 2 的平方根的倒数（约等于 0.707）。

```
Math.SQRT1_2
//0.7071067811865476
```

### 24.Math.SQRT2
说明：返回 2 的平方根（约等于 1.414）
```
Math.SQRT2
//1.4142135623730951
```

### 25.计算x 轴到点 (x,y) 之间的角度
语法：Math.atan2(y,x);
注意：参数x,y分别对应x,y坐标，注意在atant2方法里面的书写顺序
返回值：-PI 到 PI 之间的值，是从 X 轴正向逆时针旋转到点 (x,y) 时经过的角度。这里得到的是弧度哦!
```
Math.atan2(4,4)
//0.7853981633974483

Math.atan2(4,4)*(180/Math.PI)
//45
```