## 基础
#### 准备画布
```
<canvas width="600" height="400"></canvas>
```
#### 准备绘制工具
```
// 准备绘图工具
var myCanvas = document.querySelector('canvas')
var ctx = myCanvas.getContext('2d')//绘制3d的视乎使用web gl
```
#### 使用工具绘图
```
ctx.moveTo(50,50)
ctx.lineTo(100,100)
ctx.stroke();
```
## 样式
由于画线的中心对应于一个像素点的刻度，即一条线占用了两个像素各一半，因此画图默认样式显示为灰色，2px；可以通过将位置上移或者下移0.5px；
#### strokeStyle
设置描边的线条的颜色，该属性会对上面的设置进行覆盖，可通过绘制工具的beginPath()来开启新路径
#### lineWidth
设置线条的宽度
#### lineCap
设置线条是圆角或者方形，取值butt(默认) square round
#### fillStyle
#### lineJoin
设置两条线条相交点样式，取值miter、round、bevel
#### setLineDash()
设置线条为虚线样式，接受参数为数组，可以设置虚线和实线长度，如[5]：虚实都是5；[5,10]：实为5，虚为10；[5,10,15]：实虚实
#### getLineDash()
获取不重复的一段虚线样式数据
#### lineDashOffset
设置虚线偏移，如果是正值向右偏移，否则向左偏移
## 图形填充问题
#### 非零环绕规则
- 可以解决一个图形或者多个图形相交时区域的填充问题；
- 查看一个区域是否填充，从该区域做一条射线，数与该直线相交的轨迹数，如果轨迹是顺时针轨迹则加1，否则减1
- 计算最后的结果，如果为0则该区域不填充，否则进行填充；

## 注意点
- canvas标签的宽高应该通过canvas属性进行初始化，在canvas属性中的设置是画布的宽高，在css中设置的样式设置的是 canvas盒子的宽高

## 案例

#### 案例一
```
var myCanvas = document.querySelector('canvas')
var ctx = myCanvas.getContext('2d')
ctx.beginPath() //开启新的路径
ctx.moveTo(100, 100)
ctx.lineTo(300, 100)
ctx.strokeStyle = 'blue'
ctx.stroke()

ctx.beginPath() //开启新的路径
ctx.moveTo(100, 200)
ctx.lineTo(300, 200)
ctx.strokeStyle = 'red'
ctx.lineWidth = 3
ctx.stroke()

ctx.beginPath() //开启新的路径
ctx.moveTo(100, 300)
ctx.lineTo(300, 300)
ctx.strokeStyle = '#282C34'
ctx.lineWidth = 10
ctx.stroke()
```

#### 案例二
```
var canvasObj = document.querySelector('canvas')
var ctx = canvasObj.getContext('2d')
ctx.moveTo(100,100)
ctx.lineTo(200,100)
ctx.lineTo(200,200)
ctx.closePath()//关闭路径
ctx.lineWidth=10
ctx.stroke()

//绘制三角形
// var canvasObj = document.querySelector('canvas')
// var ctx = canvasObj.getContext('2d')
// ctx.moveTo(100,100)
// ctx.lineTo(200,100)
// ctx.lineTo(200,200)
// ctx.closePath()//关闭路径
// ctx.lineWidth=10
// ctx.stroke()

//绘制正方形
var canvasObj = document.querySelector('canvas')
var ctx = canvasObj.getContext('2d')
ctx.moveTo(100, 100)
ctx.lineTo(300, 100)
ctx.lineTo(300, 300)
ctx.lineTo(100, 300)
ctx.closePath()

ctx.moveTo(150, 150)
ctx.lineTo(150, 250)
ctx.lineTo(250, 250)
ctx.lineTo(250, 150)
ctx.closePath()

ctx.stroke()
ctx.fill()
```
