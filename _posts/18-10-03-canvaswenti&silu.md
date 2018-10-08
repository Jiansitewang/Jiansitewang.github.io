---
layout:     post
title:      "[JS]canvas做画板思路&问题(草稿)"
subtitle:   ""
date:       2018-10-03
author:     "WaK"
header-img: "img/post-bg-hello.jpg"
tags:
    - JavaSript
    - 学习总结
---
## 思路

在电脑上画画的分解动作其实就是 按下鼠标-一致按着拖动-松开鼠标

按下鼠标

```javascript
document.onmousedown = function(1){
    console.log(1)
}
```

此时在页面内是单击鼠标会log出”1“

而如果我们给一个参数就可以打印出相关的MouseEvent

```javascript
document.onmousedown = function(x){
    console.log(x)
}
```

log出的是一个MouseEvent，其中两个





document.onmousedown

document.onmousemove

document.onmouseup

canvas的画布栅格以及坐标空间

![img](https://mdn.mozillademos.org/files/224/Canvas_default_grid.png)

重要思路：

拖动鼠标画画  需要一个标记（声明一个新的变量） 标记是否处于画画状态 如果处于画画状态就执行画画代码反之则停止画画

重要bug：

onmousemove触发间隔是固定的，所以如果鼠标移动很快,onmousemove就不能及时触发

解决方案就是 不用别的元素来画画（如div）

用canvas元素来进行绘制



重要bug：

用css改变canvas宽高不好，会像放大图片那样，按比例放大（失真）

解决办法：用document.documentElement.clientWidth/Height来获得屏幕宽高

然后让屏幕宽高等于canvas的width和height

重要bug：

但用上面bug的解决方法之后，会产生新的bug

当用户手动改变当前页面宽度后，canvas的宽度又会变得很奇怪



这时候就需要用window.onresize（）监听resize，每次用户改变页面宽度后，就调用onresize方法，按上述方法重新设置canvas宽高



重要bug：

手机上不能画画。

做一个设备检测，如果支持touch事件就用touchAPI

2、

```javascript
if (document.body.ontouchstart !== undefined)
```

3、也可以检测touchstart是否在document.body里



Canvas.ontouchstart

Canvas.ontouchmove

Canvas.ontouchend

gap x

Width y

2x+3y =90







-------------------------------------------------------------------------------------------------------------------------------

重要api：

[`fillRect(x, y, width, height)`](https://developer.mozilla.org/zh-CN/docs/Web/API/CanvasRenderingContext2D/fillRect)

绘制一个填充的矩形

[`strokeRect(x, y, width, height)`](https://developer.mozilla.org/zh-CN/docs/Web/API/CanvasRenderingContext2D/strokeRect)

绘制一个矩形的边框

[`clearRect(x, y, width, height)`](https://developer.mozilla.org/zh-CN/docs/Web/API/CanvasRenderingContext2D/clearRect)

清除指定矩形区域，让清除部分完全透明。



绘制路径：

1. 首先，你需要创建路径起始点。
2. 然后你使用[画图命令](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D#Paths)去画出路径。
3. 之后你把路径封闭。
4. 一旦路径生成，你就能通过描边或填充路径区域来渲染图形。



```
beginPath()
```

新建一条路径，生成之后，图形绘制命令被指向到路径上生成路径。

```
closePath()
```

闭合路径之后图形绘制命令又重新指向到上下文中。

```
stroke()
```

通过线条来绘制图形轮廓。

```
fill()
```

通过填充路径的内容区域生成实心的图形。



移动笔触

```
moveTo(*x*, *y*)
```

将笔触移动到指定的坐标x以及y上。



绘制直线

[`lineTo(x, y)`](https://developer.mozilla.org/zh-CN/docs/Web/API/CanvasRenderingContext2D/lineTo)

绘制一条从当前位置到指定x以及y位置的直线。



绘制圆

[`arc(x, y, radius, startAngle, endAngle, anticlockwise)`](https://developer.mozilla.org/zh-CN/docs/Web/API/CanvasRenderingContext2D/arc)

画一个以（x,y）为圆心的以radius为半径的圆弧（圆），从startAngle开始到endAngle结束，按照anticlockwise给定的方向（默认为顺时针）来生成。

方法有六个参数：`x,y`为绘制圆弧所在圆上的圆心坐标。`radius`为半径。`startAngle`以及`endAngle`参数用弧度定义了开始以及结束的弧度。这些都是以x轴为基准。参数`anticlockwise`为一个布尔值。为true时，是逆时针方向，否则顺时针方向。



绘制矩形

- `rect(*x*, *y*, *width*, *height*)`

  绘制一个左上角坐标为（x,y），宽高为width以及height的矩形。

当该方法执行的时候，moveTo()方法自动设置坐标参数（0,0）。也就是说，当前笔触自动重置回默认坐标。

------------------------------------------------------------------------------------------------------------------------------------------------------



