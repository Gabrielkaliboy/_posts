---
title: WdatePicker(My97DatePicker)
date: 2017-06-19 09:09:40
categories: 前端
tags: [前端开发插件,javascript,vue]
---
<Excerpt in index | 首页摘要> 
vue.js开发文档：https://cn.vuejs.org/v2/guide/
<!-- more -->
<The rest of contents | 余下全文>

-----

#### 1.介绍

##### 1.1
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <script src="https://unpkg.com/vue/dist/vue.js"></script>
    <title>Document</title>
</head>
<body>
    <div id="app">
        {{message}}
    </div>
</body>
<script>
    var app=new Vue({
        el:'#app',
        data:{
            message:"你好",
        },
    });
</script>
</html>
```
##### 1.2 声明式渲染：v-bind的使用
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <script src="vue.js"></script>
    <title>Document</title>
</head>
<body>
    <div id="div1">
        <span v-bind:title="message">鼠标停留几秒试试</span>
    </div>
</body>
<script>
    var div1=new Vue({
        el:"#div1",
        data:{
            message:"这个页面加载于"+new Date(),
        },
    });
</script>
</html>
```

##### 1.3 条件与循环 v-if
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <script src="https://unpkg.com/vue/dist/vue.js"></script>
    <title>Document</title>
</head>
<body>
    <div id="app">
        <p v-if="seen">哈哈哈哈</p>
    </div>
</body>
<script>
    var app=new Vue({
        el:"#app",
        data:{
            seen:false,
            //在控制台写入app.seen=true试试
        },
    });
</script>
</html>
```

##### 1.4 v-for,数组遍历（dom遍历） 
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="vue.js"></script>
</head>
<body>
    <div id="app">
        <ol>
            <li v-for="todo in todos">
                {{todo.text}}
            </li>
        </ol>
    </div>
</body>
<script>
    //在控制台输入app.todos.push({"text":"你大爷"})
    var app=new Vue({
        el:"#app",
        data:{
            todos:[
                {"text":"哈哈哈哈哈哈哈"},
                {"text":"ni hao ma "},
                {"text":"嘎嘎嘎嘎"},
            ],
        },
    });
</script>
</html>
```

##### 1.5 v-on,处理用户输入,记得methods是有s的
为了让用户和你的应用进行互动，我们可以用 v-on 指令绑定一个事件监听器，通过它调用我们 Vue 实例中定义的方法：
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="https://unpkg.com/vue/dist/vue.js"></script>
</head>
<body>
    <div id="app">
        <p>{{message}}</p>
        <button v-on:click="reverseMessage">点击我试试</button>
    </div>
</body>
<script>
    var app=new Vue({
        el:"#app",
        data:{
            message:"你好",
        },
        methods:{
            reverseMessage:function(){
                this.message=this.message.split("").reverse().join('');
                //这里的this应该是app
            },
        },
    });
</script>
</html>
```

##### 1.5 v-model双向数据绑定
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <script src="https://unpkg.com/vue/dist/vue.js"></script>
    <title>Document</title>
</head>
<body>
    <div id="app">
        <p>{{message}}</p>
        <input type="password" v-model="message">
    </div>
</body>
<script>
    var app=new Vue({
        el:"#app",
        data:{
            message:"哈哈哈哈",
        },
    });
</script>
</html>
```

##### 1.5 组件化应用构建
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <script src="https://unpkg.com/vue/dist/vue.js"></script>
    <title>Document</title>
</head>
<body>
    <div id="app">
        <ol>
            <todo-item v-for="item in groceryList" v-bind:todo="item"></todo-item>
        </ol>
    </div>
    <script>
        Vue.component('todo-item',{
            props:['todo'],
            template:'<li>{{todo.text}}</li>'
        });
        var app=new Vue({
            el:"#app",
            data:{
                groceryList:[
                    {text:"胡萝卜"},
                    {text:"白菜"},
                    {text:"土豆"},
                    {text:"随便其他的蔬菜"}
                ]
            },
        });
    </script>
</body>
</html>
```