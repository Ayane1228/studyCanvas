# canvas

canvas元素用于使用JavaScript在网页上绘制图片,提供了一块画布.

> canvas兼容IE9以上以及主流浏览器,如果浏览器不支持canvas则可以在`<canvas>`和`</canvas>`中间可以看到相应内容,若支持则不可以看到标签中的内容.
>
> 也通过JS来进行判断,`getContext`:获取**渲染上下文**,这里可以理解成画笔.
>
> ```html
> <!DOCTYPE html>
> <html lang="en">
> <head>
>     <meta charset="UTF-8">
>     <meta http-equiv="X-UA-Compatible" content="IE=edge">
>     <meta name="viewport" content="width=device-width, initial-scale=1.0">
>     <title>Document</title>
> </head>
> <body>
>     <h1>Hello canvas</h1>
>     <canvas width="300" height="150" id="myCanvas">
> 
>     </canvas>
>     <script>
>         var myCanavas = document.querySelector("#myCanvas");
>         if (myCanavas.getContext) {
>             // 说明支持canvas
>             alert("支持canvas")
>         } else {
>             alert("不支持canvas，请升级浏览器")
>         }
>     </script>
> </body>
> </html>
> ```

## 示例

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>canvas</title>
    <style>
        body {
            text-align: center;
            padding-top: 20px;
        }

        canvas {
            box-shadow: 0 0 10px #333;
            margin: 0 auto;
        }
    </style>
</head>

<body>
    <canvas width="800" height="600" id="myCanvas">

    </canvas>
    <script>
        window.onload = function () {
            var myCanavas = document.querySelector("#myCanvas");
            if (myCanavas.getContext) {
                // 获取画笔
                var ctx = myCanavas.getContext('2d');
                // 设置颜色
                ctx.fillStyle = "#ff0000";
                // 填充画布
                // cvsCtx.fillRect(x, y, width, height);距离左上角的x,y距离,canvas图像的宽高
                ctx.fillRect(10, 10, 350, 300);
                ctx.fillStyle = "#66ff00";
                ctx.fillRect(30,30,450,450);
            }
        }
    </script>
</body>

</html>
```

> 定义一个`canvas`标签之后，获取它的渲染上下文(`getContext()`)并设置`canvas`的颜色(`ctx.fillStyle()`)、相对于左上角的位置、大小（` cvsCtx.fillRect(x, y, width, height)`可以绘制一个实色的矩形,`strokeRect()`:可以绘制一个只有边框颜色的矩形）。

## 清除矩阵

`ctx.clearRect()`:语法与`fillRect()`一致，可以清除指定位置的矩形.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>canvas</title>
    <style> 
        body{
            text-align: center;
            padding-top: 20px;
        }
        canvas{
            box-shadow: 0 0 10px #333;
            margin: 0 auto;
        }

    </style>
</head>
<body>
    <canvas width="800" height="800" id="myCanvas">
    </canvas>
    <script>
    window.onload = function(){
        var myCanavas = document.querySelector("#myCanvas");
            if (myCanavas.getContext) {
                // 获取画笔
                var ctx = myCanavas.getContext('2d');
                ctx.fillRect(80,80,300,300);
                // 清除矩阵,与fillRect语法一致
                ctx.clearRect(155,155,150,150);
                ctx.strokeRect(182.5,182.5,95,95);
            } 
    }
    </script>
</body>
</html>
```

## 绘制路径

图形的基本组成就是路径,路径的绘制一般分为四步:

1. 创建路径、创建起始点

   `beginPath()`:创建路径

   `moveTo(x,y)`创建起始点距左上角的位置

2. 使用画图命令画出路径

   `lineTo(x,y)`:路径要去的坐标

3. 把路径闭合

   即最终的坐标要与起始坐标相同

   可以直接使用`closePath()`方法直接实现闭合

4. 通过描边或填充显示图形

   `fill()`或`stroke()`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>canvas</title>
    <style> 
        body{
            text-align: center;
            padding-top: 20px;
        }
        canvas{
            box-shadow: 0 0 10px #333;
            margin: 0 auto;
        }

    </style>
</head>
<body>
    <canvas width="800" height="600" id="myCanvas">

    </canvas>
    <script>
        /*

        3. 把路径闭合
        即最终的坐标要与起始坐标相同

        */
    window.onload = function(){
        var myCanavas = document.querySelector("#myCanvas");
            if (myCanavas.getContext) {
                // 获取画笔
                var ctx = myCanavas.getContext('2d');
                //  1. 创建路径、创建起始点
                // beginPath():创建路径
                // moveTo(x,y)创建起始点距左上角的位置
                ctx.beginPath();
                ctx.moveTo(50,50);
                //  2. 使用画图命令画出路径
                // lineTo(x,y):路径要去的坐标
                ctx.lineTo(100,100);
                ctx.lineTo(100,50);
                //  3. 把路径闭合
                // 即最终的坐标要与起始坐标相同：可以直接使用closePath()方法直接实现闭合
                ctx.closePath();
                //  4. 通过描边或填充显示图形
                // fill()或stroke()
                ctx.stroke();

                ctx.beginPath();
                ctx.moveTo(125,50);
                ctx.lineTo(125,100);
                ctx.lineTo(175,50);
                ctx.closePath();
                ctx.fill();
            } 
    }   
    </script>
</body>
</html>
```

## 绘制圆型

圆 / 圆弧 的组成:

- 圆心
- 半径
- 开始角度
- 结束角度
- 旋转方向：顺时针/逆时针

方法：`arc(x,y,radius,startAngle,endAngle,anticlockwise)`

> `radius`:半径
>
> startAngle / endAngle:为0则指从3点钟方向
>
> ​	一整个圆的角度为`2 * Math.PI`
>
> anticlockwise:boolean类型,是否顺时针,默认为false(顺时针)
