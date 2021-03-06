---
title: echarts2.0
date: 2017-06-12 16:01:40
categories: 前端
tags: [前端开发插件]
---
<Excerpt in index | 首页摘要> 
echarts2.0
<!-- more -->
<The rest of contents | 余下全文>

-----
#### 1.介绍
echarts2.0是由百度出的一款专门用于图表展示的js类库，最新版本为3.0
官网：http://echarts.baidu.com/echarts2/index.html

#### 2.使用方法
5分钟上手写ECharts的第一个图表：http://echarts.baidu.com/echarts2/doc/start.html
实例集合：http://echarts.baidu.com/echarts2/doc/example.html
API：http://echarts.baidu.com/echarts2/doc/doc.html

一个简单的饼图实例，对一些常用的参数做了解释

![](https://github.com/Gabrielkaliboy/images/blob/master/_posts/echarts2.0/1.gif?raw=true)
```html
<!DOCTYPE html>
<head>
    <meta charset="utf-8">
    <title>ECharts</title>
</head>
<body>
    <!-- 为ECharts准备一个具备大小（宽高）的Dom -->
     <div id="main" style="height:300px;width:100%; min-width:700px;"></div>
    <!-- ECharts单文件引入 -->
    <script src="http://echarts.baidu.com/build/dist/echarts.js"></script>
    <script type="text/javascript">
    function pieInit(id){
        // 路径配置
        require.config({
            paths: {
                //引入模块，需要什么就引入什么
                echarts: 'http://echarts.baidu.com/build/dist'
            }
        });
        
        // 使用
        require(
            [
                'echarts',
                'echarts/chart/pie' // 使用柱状图就加载bar模块，按需加载
            ],
            function (ec) {
                // 基于准备好的dom，初始化echarts图表
                var myChart = ec.init(document.getElementById(id)); 
                var option = {
                        //用来设置标题
                        title : {
                            text: '某站点用户访问来源',
                            subtext: '纯属虚构',
                            x:'center'
                        },
                        //鼠标划到图表上面的时候，提示信息
                        tooltip : {
                            trigger: 'item',
                            formatter: "{a} <br/>{b} : {c} ({d}%)"
                        },
                        //图例，每个图表最多仅有一个图例
                        legend: {
                            orient : 'vertical',
                            x : 'left',
                            data:['直接访问','邮件营销','联盟广告','视频广告','搜索引擎']
                        },
                        //工具箱，每个图表只有一个，比如将图保存为图片等等
                        toolbox: {
                            show : true,
                            feature : {
                                mark : {show: true},
                                dataView : {show: true, readOnly: false},
                                magicType : {
                                    show: true, 
                                    type: ['pie', 'funnel'],
                                    option: {
                                        funnel: {
                                            x: '25%',
                                            width: '50%',
                                            funnelAlign: 'left',
                                            max: 1548
                                        }
                                    }
                                },
                                restore : {show: true},
                                saveAsImage : {show: true}
                            }
                        },
                        //是否启用值域漫游
                        calculable : true,
                        //查看对应的series，驱动图表生成的数据内容数组，数组中每一项为一个系列的选项及数据：
                        series : [
                            {
                                //鼠标划上去的时候显示的信息
                                name:'访问来源',
                                //图标类型
                                type:'pie',
                                //对应的饼图的大小
                                radius : '55%',
                                //饼图所处的相对位置
                                center: ['50%', '60%'],
                                data:[
                                    {value:335, name:'直接访问'},
                                    {value:310, name:'邮件营销'},
                                    {value:234, name:'联盟广告'},
                                    {value:135, name:'视频广告'},
                                    {value:1548, name:'搜索引擎'}
                                ]
                            }
                        ]
                    };
                                            
                // 为echarts对象加载数据 
                myChart.setOption(option); 
                //想让图标根据窗口变化而变化，结果不好使
                //window.onresize = mychart.resize;
            }
        );
    };
    //页面一加载就显示图表
    pieInit("main");
    //页面窗口发生变化的时候，动态加载图表以自适应
    //jquery的
    // $(window).resize(function () {    
        //pieInit("main");   
    // });
    window.onresize=function(){
        pieInit("main");
    };
    </script>
</body>
```

#### 3.与后台进行数据交互
注意查看不同的图表接收的数据格式不同：http://echarts.baidu.com/echarts2/doc/doc.html#SeriesMarkLineData
2.html
```html
<!DOCTYPE html>
<head>
    <meta charset="utf-8">
	<script src="https://cdn.bootcss.com/jquery/1.10.2/jquery.js"></script>
    <title>ECharts</title>
</head>
<body>
    <!-- 为ECharts准备一个具备大小（宽高）的Dom -->
     <div id="main" style="height:300px;width:100%; min-width:700px;"></div>
    <!-- ECharts单文件引入 -->
    <script src="http://echarts.baidu.com/build/dist/echarts.js"></script>
    <script type="text/javascript">
    function pieInit(id,data){
        // 路径配置
        require.config({
            paths: {
                //引入模块，需要什么就引入什么
                echarts: 'http://echarts.baidu.com/build/dist'
            }
        });
        
        // 使用
        require(
            [
                'echarts',
                'echarts/chart/pie' // 使用柱状图就加载bar模块，按需加载
            ],
            function (ec) {
                // 基于准备好的dom，初始化echarts图表
                var myChart = ec.init(document.getElementById(id)); 
                var option = {
                        //用来设置标题
                        title : {
                            text: '某站点用户访问来源',
                            subtext: '纯属虚构',
                            x:'center'
                        },
                        //鼠标划到图表上面的时候，提示信息
                        tooltip : {
                            trigger: 'item',
                            formatter: "{a} <br/>{b} : {c} ({d}%)"
                        },
                        //图例，每个图表最多仅有一个图例
                        legend: {
                            orient : 'vertical',
                            x : 'left',
                            data:['直接访问','邮件营销','联盟广告','视频广告','搜索引擎']
                        },
                        //工具箱，每个图表只有一个，比如将图保存为图片等等
                        toolbox: {
                            show : true,
                            feature : {
                                mark : {show: true},
                                dataView : {show: true, readOnly: false},
                                magicType : {
                                    show: true, 
                                    type: ['pie', 'funnel'],
                                    option: {
                                        funnel: {
                                            x: '25%',
                                            width: '50%',
                                            funnelAlign: 'left',
                                            max: 1548
                                        }
                                    }
                                },
                                restore : {show: true},
                                saveAsImage : {show: true}
                            }
                        },
                        //是否启用值域漫游
                        calculable : true,
                        //查看对应的series，驱动图表生成的数据内容数组，数组中每一项为一个系列的选项及数据：
                        series : [
                            {
                                //鼠标划上去的时候显示的信息
                                name:'访问来源',
                                //图标类型
                                type:'pie',
                                //对应的饼图的大小
                                radius : '55%',
                                //饼图所处的相对位置
                                center: ['50%', '60%'],
                                data:data
                            }
                        ]
                    };
                                            
                // 为echarts对象加载数据 
                myChart.setOption(option); 
                //想让图标根据窗口变化而变化，结果不好使
                //window.onresize = mychart.resize;
            }
        );
    };
    $.ajax({
    	type:"GET",
    	url:"data.json",
    	cache:false,
    	dataType:"json",
    	success: function(data){
    		 pieInit("main",data);
    		 window.onresize=function(){ pieInit("main",data); };
    	}
    });

    </script>
</body>
```
data.json
```json
[
    {
        "value": 335,
        "name": "直接访问"
    },
    {
        "value": 310,
        "name": "邮件营销"
    },
    {
        "value": 234,
        "name": "联盟广告"
    },
    {
        "value": 135,
        "name": "视频广告"
    },
    {
        "value": 1548,
        "name": "搜索引擎"
    }
]
```