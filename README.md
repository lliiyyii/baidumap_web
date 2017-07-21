# baidumap_web
>接入百度地图接口
>
>添加一些百度地图的控件
>
>百度地图的定位功能
```html
<html>
<head>
    <meta name="viewport" content="initial-scale=1.0, user-scalable=no" />
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>Hello, World</title>
    <script src="http://code.jquery.com/jquery-1.11.0.min.js"></script>
    <style type="text/css">
        html {
            height: 100%
        }
        body {
            height: 100%;
            margin: 0px;
            padding: 0px
        }
        #container {
            height: 80%
        }
    </style>
    <!-- //此为v1.4版本及以前版本的引用方式
    <script type="text/javascript" src="http://api.map.baidu.com/api?v=1.4"></script> -->
    <!-- //此为v1.5版本以后的引用方式 //-->
    <script type="text/javascript"
            src="http://api.map.baidu.com/api?v=2.0&ak=密钥">
    </script>


    <script type="text/javascript">
        var map;
        var top_left =BMAP_ANCHOR_TOP_LEFT//左上角

       function first() {
            navigator.geolocation.getCurrentPosition(init);//获取定位
        }


        function init(position){
            var currentLat = position.coords.latitude;//经度
            var currentLon = position.coords.longitude;//纬度
            var point = new BMap.Point(currentLon,currentLat);//经纬度确定点

            load(point);
            setMapEvent();
            addMapControl();
        }

        function load(point) {

            // BMap是百度地图API的命名空间，所有的类都在这里面
            map = new BMap.Map("container"); // 创建一个Map对象

            map.centerAndZoom(point, 15);//初始地图显示为位置

            map.addOverlay(new BMap.Marker(point));//当前位置加标记
            // 两秒钟后移动到中心点
            window.setTimeout(function() {
                map.panTo
                map.panTo(new BMap.Point(116.415, 39.918));
            }, 2000);

            map.addControl(new BMap.MapTypeControl()); //添加地图类型控件 ()
            map.addControl(new BMap.ScaleControl());
        }
        //添加控件
        function setMapEvent(){

            map.enableDragging();//启动地图拖拽事件，默认启用
            map.enableScrollWheelZoom();//启动地图滚轮放大缩小
            map.enableDoubleClickZoom();//启动鼠标双击放大
            map.enableKeboard();//启用键盘上下左右键移动地图
            map.addControl(new BMap.MapTypeControl());//调用卫星地图
            map.addControl(new BMap.ScaleControl({auchor:top_left}));//比例尺
            map = new BMap.Map("container",{mapType: BMAP_SATELLITE_MAP});
            map.addControl(new BMapScaleControl({author:BMAP_NAVIGATION_CONTROL_ZOOM}));//添加比例尺
        }



    </script>
</head>
<body onload="first()">

<div id="container"></div>
<div id=" content">
    <p></p>
</div>
</body>
</html>
```
