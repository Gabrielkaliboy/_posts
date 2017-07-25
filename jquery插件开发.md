---
title: jquery插件
date: 2017-07-25 19:38:40
categories: 前端
tags: [javascript,jquery]
---
<Excerpt in index | 首页摘要> 
jquery插件
<!-- more -->
<The rest of contents | 余下全文>

-----

### 1.jQuery插件开发模式
根据《jQuery高级编程》的描述，jQuery插件开发方式主要有三种：
- 通过$.extend()来扩展jQuery,只能通过$调用，不能利用jQuery强大的选择器
- 通过$.fn 向jQuery添加新的方法
- 通过$.widget()应用jQuery UI的部件工厂方式创建

通常我们使用第二种方法来进行简单插件开发，说简单是相对于第三种方式。第三种方式是用来开发更高级jQuery部件的，该模式开发出来的部件带有很多jQuery内建的特性，比如插件的状态信息自动保存，各种关于插件的常用方法等，非常贴心，这里不细说。

而第一种方式又太简单，仅仅是在jQuery命名空间或者理解成jQuery身上添加了一个静态方法而以。所以我们调用通过$.extend()添加的函数时直接通过$符号调用（$.myfunction()）而不需要选中DOM元素($('#example').myfunction())。请看下面的例子。
```javascript
$.extend({
    sayHello:function(name){
        console.log("hello"+(name ? "  "+name : "  boy")+"!");
    }
});
$.sayHello();//调用 hello  boy!
$.sayHello("Gabriel");//带参数调用 hello  Gabriel!
```

上面代码中，通过$.extend()向jQuery添加了一个sayHello函数，然后通过$直接调用。到此你可以认为我们已经完成了一个简单的jQuery插件了。

但如你所见，这种方式用来定义一些辅助方法是比较方便的。比如一个自定义的console，输出特定格式的信息，定义一次后可以通过jQuery在程序中任何需要的地方调用它。

```javascript
    $.extend({
        log:function(message){
            var now = new Date(),
                y=now.getFullYear(),
                m=now.getMonth()+1,//javascript中月份是在0开始的
                d=now.getDate(),
                h=now.getHours(),
                min=now.getMinutes(),
                s=now.getSeconds(),
                time=y+"年"+m+"月"+d+"日"+h+"时"+min+"分"+s+"秒";
                alert(time+message);
        }
    })
    $.log("你好");
```
但这种方式无法利用jQuery强大的选择器带来的便利，要处理DOM元素以及将插件更好地运用于所选择的元素身上，还是需要使用第二种开发方式。你所见到或使用的插件也大多是通过此种方式开发。

### 2.插件开发
下面我们就来看第二种方式的jQuery插件开发。

#### 2.1基本方法
```javascript
$.fn.pluginName = function() {
    //your code goes here
}
```
基本上就是往$.fn上面添加一个方法，名字是我们的插件名称。然后我们的插件代码在这个方法里面展开。

比如我们将页面上所有链接颜色转成红色，则可以这样写这个插件：
```javascript
$.fn.myPlugin = function() {
    //在这里面,this指的是用jQuery选中的元素
    //example :$('a'),则this=$('a')
    this.css('color', 'red');
}
```
在插件名字定义的这个函数内部，this指代的是我们在调用该插件时，用jQuery选择器选中的元素，一般是一个jQuery类型的集合。比如$('a')返回的是页面上所有a标签的集合，且这个集合已经是jQuery包装类型了，也就是说，在对其进行操作的时候可以直接调用jQuery的其他方法而不需要再用美元符号来包装一下。

所以在上面插件代码中，我们在this身上调用jQuery的css()方法，也就相当于在调用 $('a').css()。

理解this在这个地方的含义很重要。这样你才知道为什么可以直接商用jQuery方法同时在其他地方this指代不同时我们又需要用jQuery重新包装才能调用，下面会讲到。初学容易被this的值整晕，但理解了就不难。

现在就可以去页面试试我们的代码了，在页面上放几个链接，调用插件后链接字体变成红色。
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <script src="https://cdn.bootcss.com/jquery/2.0.3/jquery.min.js"></script>
    <title>Document</title>
</head>
<body>
    <ul>
        <li>
            <a href="http://www.webo.com/liuwayong">我的微博</a>
        </li>
        <li>
            <a href="http://http://www.cnblogs.com/Wayou/">我的博客</a>
        </li>
        <li>
            <a href="http://wayouliu.duapp.com/">我的小站</a>
        </li>
    </ul>
    <p>这是p标签不是a标签，我不会受影响</p>
</body>
<script>
    $.fn.myPlug = function(){
        //这里的this指向的是用jQuery选中的元素
        //example :$('a'),则this=$('a')
        this.css('color','red');
    }

    $(function(){
        //页面中所有的被a元素包裹的都变成了红色
        $("a").myPlug();
    })
</script>
</html>
```

下面进一步，在插件代码里处理每个具体的元素，而不是对一个集合进行处理，这样我们就可以针对每个元素进行相应操作。

我们已经知道this指代jQuery选择器返回的集合，那么通过调用jQuery的.each()方法就可以处理合集中的每个元素了，但此刻要注意的是，在each方法内部，this指带的是普通的DOM元素了，如果需要调用jQuery的方法那就需要用$来重新包装一下。

比如现在我们要在每个链接显示链接的真实地址，首先通过each遍历所有a标签，然后获取href属性的值再加到链接文本后面。

更改后我们的插件代码为：
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <script src="https://cdn.bootcss.com/jquery/2.0.3/jquery.min.js"></script>
    <title>Document</title>
</head>
<body>
    <ul>
        <li>
            <a href="http://www.webo.com/liuwayong">我的微博</a>
        </li>
        <li>
            <a href="http://http://www.cnblogs.com/Wayou/">我的博客</a>
        </li>
        <li>
            <a href="http://wayouliu.duapp.com/">我的小站</a>
        </li>
    </ul>
    <p>这是p标签不是a标签，我不会受影响</p>
</body>
<script>
    $.fn.myPlug = function(){
        //这里的this指向的是用jQuery选中的元素
        //example :$('a'),则this=$('a')
        this.css('color','red');
        this.each(function(){
            //对每个元素进行操作
            $(this).append(""+$(this).attr("href"))
        });
    }

    $(function(){
        //页面中所有的被a元素包裹的都变成了红色
        $("a").myPlug();
    })
</script>
</html>
```
到此，你已经可以编写功能简单的jQuery插件了。是不是也没那么难。

下面开始jQuery插件编写中一个重要的部分，参数的接收。

### 3.支持链式调用
我们都知道jQuery一个时常优雅的特性是支持链式调用，选择好DOM元素后可以不断地调用其他方法。

要让插件不打破这种链式调用，只需return一下即可。
```javascript
$.fn.myPlugin = function() {
    //在这里面,this指的是用jQuery选中的元素
    this.css('color', 'red');
    return this.each(function() {
        //对每个元素进行操作
        $(this).append(' ' + $(this).attr('href'));
    }))
}
```

### 4.让插件接收参数(好好看看$.extend有一个深浅更改)
一个强劲的插件是可以让使用者随意定制的，这要求我们提供在编写插件时就要考虑得全面些，尽量提供合适的参数。

比如现在我们不想让链接只变成红色，我们让插件的使用者自己定义显示什么颜色，要做到这一点很方便，只需要使用者在调用的时候传入一个参数即可。同时我们在插件的代码里面接收。另一方面，为了灵活，使用者可以不传递参数，插件里面会给出参数的默认值。

在处理插件参数的接收上，通常使用jQuery的extend方法，上面也提到过，但那是给extend方法传递单个对象的情况下，这个对象会合并到jQuery身上，所以我们就可以在jQuery身上调用新合并对象里包含的方法了，像上面的例子。当给extend方法传递一个以上的参数时，它会将所有参数对象合并到第一个里。同时，如果对象中有同名属性时，合并的时候后面的会覆盖前面的。

利用这一点，我们可以在插件里定义一个保存插件参数默认值的对象，同时将接收来的参数对象合并到默认对象上，最后就实现了用户指定了值的参数使用指定的值，未指定的参数使用插件默认值。

为了演示方便，再指定一个参数fontSize，允许调用插件的时候设置字体大小。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <script src="https://cdn.bootcss.com/jquery/2.0.3/jquery.min.js"></script>
    <title>Document</title>
</head>
<body>
    <ul>
        <li>
            <a href="http://www.webo.com/liuwayong">我的微博</a>
        </li>
        <li>
            <a href="http://http://www.cnblogs.com/Wayou/">我的博客</a>
        </li>
        <li>
            <a href="http://wayouliu.duapp.com/">我的小站</a>
        </li>
    </ul>
    <p>这是p标签不是a标签，我不会受影响</p>
</body>
<script>
    $.fn.myPlug = function(options){
        var defaults={
            'color':'red',
            'fontSize':'12px'
        };
        var settings=$.extend(defaults,options);
        return this.css({
            'color':settings.color,
            'fontSize':settings.fontSize
        });
    }

    $(function(){
        //现在，我们调用的时候指定颜色，字体大小未指定，会运用插件里的默认值12px。
        $("a").myPlug({
            'color':'#00f'
        });
    })
</script>
</html>
```

### 5. 保护好默认参数
注意到上面代码调用extend时会将defaults的值改变，这样不好，因为它作为插件因有的一些东西应该维持原样，另外就是如果你在后续代码中还要使用这些默认值的话，当你再次访问它时它已经被用户传进来的参数更改了。

一个好的做法是将一个新的空对象做为$.extend的第一个参数，defaults和用户传递的参数对象紧随其后，这样做的好处是所有值被合并到这个空对象上，保护了插件里面的默认值。

```javascript
$.fn.myPlugin = function(options) {
    var defaults = {
        'color': 'red',
        'fontSize': '12px'
    };
    var settings = $.extend({},defaults, options);//将一个空对象做为第一个参数
    return this.css({
        'color': settings.color,
        'fontSize': settings.fontSize
    });
}
```
到此，插件可以接收和处理参数后，就可以编写出更健壮而灵活的插件了。若要编写一个复杂的插件，代码量会很大，如何组织代码就成了一个需要面临的问题，没有一个好的方式来组织这些代码，整体感觉会杂乱无章，同时也不好维护，所以将插件的所有方法属性包装到一个对象上，用面向对象的思维来进行开发，无疑会使工作轻松很多。





























[原文作者](http://www.cnblogs.com/Wayou/p/jquery_plugin_tutorial.html)