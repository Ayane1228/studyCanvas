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
    window.onload = function(){
        var myCanavas = document.querySelector("#myCanvas");
            if (myCanavas.getContext) {
                // 获取画笔
                var ctx = myCanavas.getContext('2d');
                // 画笔的颜色和粗细
                ctx.strokeStyle = 'blue';
                ctx.lineWidth = 10;
                ctx.beginPath();
                ctx.arc(400,300,150,0,2 * Math.PI,false);
                ctx.stroke();
                // 半圆
                ctx.beginPath();
                ctx.arc(400,300,120,0,Math.PI,true);
                ctx.stroke();
                // 四分之圆
                ctx.beginPath();
                ctx.arc(400,300,20,0,0.5*Math.PI,true);
                ctx.stroke();
                // cvsCtx.arc(x, y, r, sAngle, eAngle, false);
            } 
    }
    </script>
</body>
</html>
```

## 画笑脸

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
    window.onload = function(){
        var myCanavas = document.querySelector("#myCanvas");
            if (myCanavas.getContext) {
                // 获取画笔
                var ctx = myCanavas.getContext('2d');
                // 画笔的颜色和粗细
                ctx.strokeStyle = 'blue';
                ctx.lineWidth = 10;
                ctx.beginPath();
                ctx.arc(400,300,300,0,2 * Math.PI,false);
                ctx.stroke();
                ctx.beginPath();
                ctx.arc(300,250,50,0,2 * Math.PI,false);
                ctx.stroke();
                ctx.beginPath();
                ctx.arc(500,250,50,0,2*Math.PI,false);
                ctx.stroke();
                ctx.beginPath();
                ctx.arc(400,400,150,0,Math.PI,false);
                ctx.stroke();

            } 
    }
    </script>
</body>
</html>
```

## 线性渐变

创建线性渐变方法`cvsCtx.createLinearGradient(x0, y0, x1, y1);`

参数:起始点X1,起始点Y1,终点X2,终点Y2(是指相对于画布的坐标)

线性变化的添加颜色方法:`cvsCtx.addColorStop(stop(0 ~ 1), color);`

参数:表示颜色所在的相对位置,颜色 

> `ctx.fillStyle = lingrad`表示`ctx`使用这个`linggrad`样式

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
    window.onload = function(){
        var myCanavas = document.querySelector("#myCanvas");
            if (myCanavas.getContext) {
                // 获取画笔
                var ctx = myCanavas.getContext('2d');
                // cvsCtx.createLinearGradient(x0, y0, x1, y1);创建线性渐变
                var lingrad = ctx.createLinearGradient(0, 0, 200, 200);
                // cvsCtx.addColorStop(stop(0 ~ 1), color);线性变化的添加颜色方法:
                lingrad.addColorStop(0,"black");
                lingrad.addColorStop("0.3","magenta");
                lingrad.addColorStop("0.5","blue");
                lingrad.addColorStop("0.6","green");
                lingrad.addColorStop("0.8","yellow");
                lingrad.addColorStop(1,"red");
                // 表示ctx使用这个linggrad样式
                ctx.fillStyle = lingrad;
                // 绘制图形
                ctx.fillRect(10,10,200,200);
                var lingrad2 = ctx.createLinearGradient(50,50,150,150);
                lingrad2.addColorStop(0,"black");
                lingrad2.addColorStop(1,"white");
                ctx.strokeStyle = lingrad2;
                ctx.strokeRect(35,35,150,150)
            } 
    }
    </script>
</body>
</html>
```

## 径向渐变(创建放射状/环形的渐变)

方法：·`context.createRadialGradient(x0,y0,r0,x1,y1,r1); `

参数:

1. 渐变的开始圆心的 x 坐标
2.  渐变的开始圆心的 y 坐标
3. 开始圆的半径
4. 渐变的结束圆的心 x 坐标
5. 渐变的结束圆心的 y 坐标
6. 结束圆的半径

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
    window.onload = function(){
        var myCanavas = document.querySelector("#myCanvas");
            if (myCanavas.getContext) {
                // 获取画笔
                var ctx = myCanavas.getContext('2d');
                var grad = ctx.createRadialGradient(400,300,100,400,300,200)
                grad.addColorStop(0,"blue");
                grad.addColorStop(0.5,"red");
                grad.addColorStop(0.8,"pink");
                grad.addColorStop(0.9,"pink");
                grad.addColorStop(1,"green");
                // 确定绘制的渐变样式
                ctx.fillStyle = grad;
                ctx.fillRect(400,300,200,200);
            } 
    }
    </script>
</body>
</html>
```

## 绘制图片

将图片渲染到画布中

方法`cvsCtx.createPattern(image, repetition);`

参数:

1. img元素
2. 是否`repeat`,以及`repeat`方向：`repeat|repeat-x|repeat-y|no-repeat`

> 在绘制图像时一定要确保图片已经加载完成

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
    window.onload = function(){
        var myCanavas = document.querySelector("#myCanvas");
            if (myCanavas.getContext) {
                // 获取画笔
                var ctx = myCanavas.getContext('2d');
                // cvsCtx.createPattern(image, repetition);
                var myImg = new Image();
                myImg.src = "https://static.chiphell.com/forum/202107/03/231037wnilp6ggu9x7pg95.jpg";
                myImg.onload = function() {
                    var parn =  ctx.createPattern(myImg,"no-repeat");
                    ctx.fillStyle = parn;
                    ctx.fillRect(0,0,800,600);
                }
            } 

    }
    </script>
</body>
</html>
```

## 渲染文字

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
    window.onload = function(){
        var myCanavas = document.querySelector("#myCanvas");
            if (myCanavas.getContext) {
                // 获取画笔上下文
                var ctx = myCanavas.getContext('2d');
                // 线性渐变的颜色 
                // 开始/结束的X,Y轴位置
                // cvsCtx.addColorStop(stop(0 ~ 1), color); 渐变颜色设置
                var lin = ctx.createLinearGradient(100,200,500,200);
                lin.addColorStop(0,blue);
                lin.addColorStop(0.5,green);
                lin.addColorStop(1,Weight);
                /*
                    阴影
                    shadowColor:字体颜色
                    shadowBlue：模糊度
                    shadowOffsetX / Y :偏移量
                */
                ctx.shadowColor = 'blue';
                ctx.shadowBlue = 50;
                ctx.shadowOffsetX = 15;
                ctx.shdowOffsetY = 15;
                // 设置字体
                /*
                cvsCtx.font = 'style, weight, size, family';
                参数：
                    fontWeight: normal,加粗bold,bolder,缩小lighter或使用数字
                    fontStyle: 文字样式:normal,italic斜体
                    fontSize: 字体大小
                    fontFamily:字体
                */
                ctx.font = 'bolder italic 80px Arial';

               // 绘制字体 字符串 开始的X,Y位置 
               ctx.fillText('BlackBird',100,100);
            } 
    }
    </script>
</body>
</html>
```

