## Canvas

### Canvas介绍

HTML5 <canvas> 标签用于绘制图像（通过脚本，通常是 JavaScript）。

不过，<canvas> 元素本身并没有绘制能力（它仅仅是图形的容器） - 您必须使用脚本来完成实际的绘图任务。

getContext() 方法可返回一个对象，该对象提供了用于在画布上绘图的方法和属性。

 getContext("2d") 对象属性和方法，可用于在画布上绘制文本、线条、矩形、圆形等等。

注意:

1. <canvas>标签是成对的,默认的宽和高是300和150

2. 如果浏览器不支持则直接在标签内部提示:您的破浏览器需要升级了

3. <canvas>只有两个属性:width和height,

4. canvas就是画布:

5. ```
   html属性设置width height时只影响画布本身不影画布内容
   css属性设置width height时不但会影响画布本身的高宽，
   还会使画布中的内容等比例缩放（缩放参照于画布默认的尺寸）
   ```

6. 渲染上下文:

   ```
   <canvas> 元素只是创造了一个固定大小的画布，要想在它上面去绘制内容，
   我们需要找到它的渲染上下文
      <canvas> 元素有一个叫做 getContext() 的方法，这个方法是用来获得渲染上下文和它的绘画功能。
   getContext()只有一个参数，上下文的格式
   ```

   getContext()中只有一个参数: getContext("2d")

   该方法返回的是:[`CanvasRenderingContext2D`](https://developer.mozilla.org/zh-CN/docs/Web/API/CanvasRenderingContext2D) 对象,所以,页面中想要使用这个对象画图的时候一定要检测浏览器是否支持,代码如下:

   ```javascript
   if(!canvas.getContext)return;这行代码没有问题了,才能写下一行(该行代码一定要写在函数中,否则报错(return的问题))
   var ctx=canvas.getContext("2d");
   此时才有绘画能力

   ```

   ​

### Canvas基本使用

```html
<body>
<canvas id="test" width="300" height="250">
  您的破浏览器不支持,请升级新的浏览器!就这玩意,爱用不用
</canvas>
<script type="text/javascript">

  //页面加载后获取画布(虽然代码写在这里,可以不需要再写onload事件,但是,我愿意)
  onload = function () {
    //获取或不
    var canvas = document.querySelector("#test");
    //检测浏览器是否支持这个对象
    if (canvas.getContext) return;
    var ctx = canvas.getContext("2d");
  };
</script>
</body>

总结:注意浏览器是否支持Canvas标签,注意浏览器是否支持绘制对象(canvas.getContext("2d"))
```



### Canvas绘制矩形

```javascript
<script type="text/javascript">

  //页面加载后获取画布(虽然代码写在这里,可以不需要再写onload事件,但是,我愿意)
  window.onload = function () {
    //获取或不
    var canvas = document.querySelector("#test");
    //检测浏览器是否支持这个对象
    if (!canvas.getContext) return;
    var ctx = canvas.getContext("2d");

    //设置绘制---画笔----描边的粗细
    ctx.lineWidth = 20;
    //设置绘制--画笔---颜色
    ctx.strokeStyle = "blue";
    //设置相连接位置的样式
    ctx.lineJoin = "bevel";//三角----


    //直接绘制一个描边的矩形(从某个点到具体的大小)========描边
    ctx.strokeRect(10, 10, 200, 100);


    //绘制一个矩形:
    /*
    *
    * 绘制矩形有三种方式:
    * fillRect();
    * strokeRect();
    * clearRect();
    * 三者参数个数和意义相同
    * 参数1:起始点的横坐标
    * 参数2:起始点的纵坐标
    * 参数3:绘制矩形的宽度
    * 参数4:绘制矩形的高度
    * 注意:这里的起始点是相对于画布(Canvas)的原点(画布自己的左上角)
    *
    * 下面这个属性设置的是连接处的样式效果
    * 绘制对象.lineJoin这个属性的值有三个: bevel---三角  round---原型  miter---直线
    *
    *
    * */

    //设置这个填充矩形的颜色
    ctx.fillStyle="yellow";
    //绘制一个填充效果的矩形
    ctx.fillRect(10,130,200,100);

    //重新绘制一个矩形--也是绘制,但是看起来是清空了---重新绘制并设置为透明效果
    //擦除了原来绘制的内容，并且所有像素变为透明了---参数:起点和范围
    ctx.clearRect(10, 10, 200, 100);
  };
</script>

总结:
fillStyle是设置填充的颜色
lineWidth是描边的宽度
lineJoin是连接位置的样式效果 bevel三角 和miter直线 和round圆
strokeStyle是设置描边的颜色

注意:
<script type="text/javascript">
    //这里需要注意一个问题:1px有可能会重叠,
    ctx.fillRect(0,0,100,100);
    //直接绘制一个描边的矩形(从某个点到具体的大小)========描边
    ctx.strokeRect(100.5, 100.5, 100, 100);
    /*
    *
    * 在100的位置上下 各自  绘制了 0.5px 导致了 最终绘制了2px
    * */
</script>
```



### Canvas绘制路径

```
图形的基本元素是路径。路径是通过不同颜色和宽度的线段或曲线相连形成的不同形状的点的集合。
```

#### 步骤:

1.设定起点 moveTo()

2.设置某个路径的连接点lineTO()

3.封闭路径closePath();

4.结束后可以进行填充或者描边渲染绘制的内容 绘制stroke()

```
beginPath()
   新建一条路径，生成之后，图形绘制命令被指向到路径上准备生成路径。
   
   生成路径的第一步叫做beginPath()。本质上，路径是由很多子路径构成，这些子路径都是在一个列表中，
   所有的子路径（线、弧形、等等）构成图形。而每次这个方法调用之后，列表清空重置，
   然后我们就可以重新绘制新的图形。

moveTo(x, y)
   将笔触移动到指定的坐标x以及y上
   当canvas初始化或者beginPath()调用后，你通常会使用moveTo()函数设置起点
   
lineTo(x, y)
   将笔触移动到指定的坐标x以及y上
   绘制一条从当前位置到指定x以及y位置的直线。

closePath()
   闭合路径之后图形绘制命令又重新指向到上下文中。
      闭合路径closePath(),不是必需的。这个方法会通过绘制一条从当前点到开始点的直线来闭合图形。
   如果图形是已经闭合了的，即当前点为开始点，该函数什么也不做
      当你调用fill()函数时，所有没有闭合的形状都会自动闭合，所以你不需要调用closePath()函数。
   但是调用stroke()时不会自动闭合
   
stroke()
   通过线条来绘制图形轮廓。
   不会自动调用closePath()
   
fill()
   通过填充路径的内容区域生成实心的图形。
   自动调用closePath()
```

#### 绘制矩形

```
rect(x, y, width, height)
   绘制一个左上角坐标为（x,y），宽高为width以及height的矩形。
   当该方法执行的时候，moveTo()方法自动设置坐标参数（0,0）。
   也就是说，当前笔触自动重置会默认坐标
```



```
lineCap
   lineCap 是 Canvas 2D API 指定如何绘制每一条线段末端的属性。
   有3个可能的值，分别是：
      butt  :线段末端以方形结束。 
      round :线段末端以圆形结束
      square:线段末端以方形结束，但是增加了一个宽度和线段相同，高度是线段厚度一半的矩形区域
   默认值是 butt。
      
save
   save() 是 Canvas 2D API 通过将当前状态放入栈中，保存 canvas 全部状态的方法
   
   保存到栈中的绘制状态有下面部分组成：
      当前的变换矩阵。
      当前的剪切区域。
      当前的虚线列表.
      以下属性当前的值： strokeStyle, 
                fillStyle,  
                lineWidth, 
                lineCap, 
                lineJoin...
                
restore
   restore() 是 Canvas 2D API 通过在绘图状态栈中弹出顶端的状态，将 canvas 恢复到最近的保存状态的方法。 
   如果没有保存状态，此方法不做任何改变。    
```

#### 签名案例

```javascript
 //页面加载
  window.onload = function () {

    //获取画板和获取绘制对象
    var canvas = document.querySelector("#test");
    if (!canvas.getContext) return;
    var ctx = canvas.getContext("2d");
    //获取鼠标按下事件,里面通过鼠标移动事件进行绘制
    canvas.onmousedown = function (e) {
      e = e || window.event;
      //全局捕获鼠标
      if(canvas.setCapture){
        canvas.setCapture();
      }

      //清理路径和定义起始点
      ctx.beginPath();
      ctx.moveTo(e.clientX-canvas.offsetLeft,e.clientY-canvas.offsetTop);
      document.onmousemove=function (evt) {

        evt = evt ||window.event;
        //保存之前的样式状态并设置新的颜色
        ctx.save();
        ctx.strokeStyle="green";

        //绘制到某个定点
        ctx.lineTo(evt.clientX-canvas.offsetLeft,evt.clientY-canvas.offsetTop);
        ctx.stroke();//绘制
        ctx.restore();//恢复之前状态

      };
    };
    //最终鼠标抬起干掉所有的事件
    canvas.onmouseup = function () {
        //干掉鼠标移动事件和释放鼠标
      document.onmousemove=document.onmouseup=null;
      if(document.releaseCapture){
        document.releaseCapture();
      }
    };

  };
```



### Canvas绘制曲线

#### 绘制圆形

### 角度与弧度的js表达式:radians=(Math.PI/180)*degrees。

### canvas绘制圆形

```
arc(x, y, radius, startAngle, endAngle, anticlockwise)
		画一个以（x,y）为圆心的以radius为半径的圆弧（圆），从startAngle开始到endAngle结束，
		按照anticlockwise给定的方向（默认为顺时针）来生成。
		ture：逆时针
		false:顺时针
	
	x,y为绘制圆弧所在圆上的圆心坐标
	radius为半径
	startAngle以及endAngle参数用弧度定义了开始以及结束的弧度。这些都是以x轴为基准
	参数anticlockwise 为一个布尔值。为true时，是逆时针方向，否则顺时针方向。

```

### arcTo

```
arcTo(x1, y1, x2, y2, radius)
根据给定的控制点和半径画一段圆弧
肯定会从(x1 y1)  但不一定经过(x2 y2);(x2 y2)只是控制一个方向
```

```javascript
//页面加载
  window.onload=function () {
    var canvas = document.querySelector("#test");
    if(!canvas.getContext)return;
    var ctx = canvas.getContext("2d");
    /*
    参数1:开始的横坐标
    参数2:开始的纵坐标
    参数3:开始的半径
    参数4:开始的弧度
    参数5:结束的弧度
    参数6:顺时针还是逆时针,默认是顺时针--false,逆时针:true
    弧度的计算公式:
    Math.PI/180*degrees---度
   */
    ctx.beginPath();//开始新的绘制路径
    //扇形
    ctx.moveTo(100,100);
    ctx.arc(100,100,50,0,180*Math.PI/180);
    ctx.closePath();
    ctx.stroke();
  };
```

#### 绘制弧形

```javascript
//页面加载
  window.onload=function () {
    var canvas = document.querySelector("#test");
    if(!canvas.getContext)return;
    var ctx = canvas.getContext("2d");
    ctx.beginPath();//开始新的绘制路径
    /*
    *
    * arcTo()参数
    * 参数1和参数2 :控制点1 坐标
    * 参数3和参数4 :控制点2坐标
    * 参数5:圆弧半径
    *
    * */
    ctx.moveTo(50,50);
    ctx.arcTo(200,50,200,200,50);//切线弧
    //ctx.lineTo(200,200);
    ctx.stroke();//绘制
  };
```

### 二次贝塞尔

```
quadraticCurveTo(cp1x, cp1y, x, y)
	绘制二次贝塞尔曲线，cp1x,cp1y为一个控制点，x,y为结束点。
	起始点为moveto时指定的点
```

### 三次贝塞尔

```
bezierCurveTo(cp1x, cp1y, cp2x, cp2y, x, y)
	绘制三次贝塞尔曲线，cp1x,cp1y为控制点一，cp2x,cp2y为控制点二，x,y为结束点。
	起始点为moveto时指定的点
```

#### 二次贝塞尔线

```javascript
//页面加载
  window.onload=function () {
    var canvas = document.querySelector("#test");
    if(!canvas.getContext)return;
    var ctx = canvas.getContext("2d");
    ctx.beginPath();//开始新的绘制路径
    //定义起始点
    ctx.moveTo(20,200);
    //定义控制点
    var cp1x=40,cp1y=100;
    //定义结束点
    var x=200,y=200;
    //控制二次贝塞尔
    ctx.quadraticCurveTo(cp1x,cp1y,x,y);
    ctx.stroke();//绘制
  };
```

#### 三次贝塞尔线

```javascript
//页面加载
  window.onload=function () {
    var canvas = document.querySelector("#test");
    if(!canvas.getContext)return;
    var ctx = canvas.getContext("2d");
    ctx.beginPath();//开始新的绘制路径
    //定义起始点
    ctx.moveTo(40,200);
    //定义控制点1
    var cp1x=20,cp1y=100;
    //定义控制点2
    var cp2x=100,cp2y=120;
    //定义终点
    var x=200,y=200;
    //控制三次贝塞尔曲线
    ctx.bezierCurveTo(cp1x,cp1y,cp2x,cp2y,x,y);
    ctx.stroke();//绘制
  };
```



### Canvas变形



```
canvas中的变换
   translate(x, y)
      我们先介绍 translate 方法，它用来移动 canvas的原点到一个不同的位置。
      translate 方法接受两个参数。x 是左右偏移量，y 是上下偏移量，
      
      在canvas中translate是累加的

   rotate(angle)
      这个方法只接受一个参数：旋转的角度(angle)，它是顺时针方向的，以弧度为单位的值。
      旋转的中心点始终是 canvas 的原点，如果要改变它，我们需要用到 translate 方法
      
      在canvas中rotate是累加的
      
   scale(x, y)
      scale 方法接受两个参数。x,y 分别是横轴和纵轴的缩放因子，它们都必须是正值。
      值比 1.0 小表示缩小，比 1.0 大则表示放大，值为 1.0 时什么效果都没有。
      缩放一般我们用它来增减图形在 canvas 中的像素数目，对形状，位图进行缩小或者放大。
      
      在canvas中scale是累称的
```

#### translate

```javascript
  //页面加载
  window.onload=function () {
    var canvas = document.querySelector("#test");
    if(!canvas.getContext)return;
    var ctx = canvas.getContext("2d");
    /*
    *
    * translate移动的是Canvas的原点坐标
    * 参数1:左右的偏移量
    * 参数2:上下的偏移量
    * 如果写了多次的translate会累加偏移量,如:
    * ctx.translate(50,50);
    * ctx.translate(50,50);
    * 此时就相当于下面的写法
    * ctx.translate(100,100);
    *
    *
    * */
    ctx.translate(100,100);
    ctx.fillRect(0,0,100,100);

  };
```

#### rotate

```javascript
 //页面加载
  window.onload=function () {
    var canvas = document.querySelector("#test");
    if(!canvas.getContext)return;
    var ctx = canvas.getContext("2d");
    ctx.translate(100,100);//移动原点坐标
    /*
    *
    * 参数:旋转的角度
    *
    * */
    ctx.rotate(Math.PI/180*45);
    ctx.fillRect(0,0,100,100);

  };
```

#### scale

```javascript
  //页面加载
  window.onload=function () {
    var canvas = document.querySelector("#test");
    if(!canvas.getContext)return;
    var ctx = canvas.getContext("2d");
    ctx.translate(100,100);//移动原点坐标
    //ctx.rotate(Math.PI/180*45);
    /*
    *
    * 参数1:横轴的缩放因子
    * 参数2:纵轴的缩放因子
    * 必须是正数(否则啥也看不到了)
    * 横轴缩放因子举例子:
    * 如果是0.5,那就一个单位的像素变成了0.5个像素,绘制出来的效果就是原来的一半
    * 同理:
    * 如果是2,那就一个单位的像素变成了2个像素,绘制出来的效果就是原来的一倍
    *
    * 缩放因子变大,画布内的css像素个数变少了,单个的css像素尺寸变大,
    * 缩放因子变小,画布内的css像素个数变多了,单个的css像素尺寸变小
    *
    * */
    ctx.scale(1,1);
    ctx.fillRect(0,0,100,100);

  };
```

#### 变换案例

```javascript
 //页面加载
  window.onload = function () {
    //获取画布和绘制对象
    var canvas = document.querySelector("#test");
    if (!canvas.getContext) return;
    var ctx = canvas.getContext("2d");
    var flag = 0;//旋转的度
    var scale = 0;//缩放的数值
    var flagScale = 0;//控制缩放的最小和最大值
    setInterval(function () {
      flag += 5;
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      //缩放和旋转
      ctx.save();
      //设置原点
      ctx.translate(300, 300);
      //旋转
      ctx.rotate(flag * Math.PI / 180);
      if (scale === 0) {
        flagScale = 1;
      } else if (scale === 100) {
        flagScale = -1;
      }
      //控制缩放的缩放因子(根据flagScale控制scale的值)
      scale += flagScale;
      //缩放
      ctx.scale(scale / 50, scale / 50);
      ctx.beginPath();
      ctx.fillRect(-100, -100, 200, 200);
      ctx.restore();
    }, 100);


  };
```





### Canvas实例:时钟



```
###表盘
   1.初始化
      将圆心调整到画布的中间
      由于canvas中画圆与旋转所参照的坐标系于正常坐标系有出入
         将整个画布逆时针旋转90度
      初始化一些样式数据
         ctx.lineWidth = 8;
         ctx.strokeStyle = "black";
         ctx.lineCap = "round";
   
   2.外层空心圆盘
      圆盘颜色:#325FA2
      圆盘宽度:14
      圆盘半径:140
      
   3.时针刻度
      长度为20
      宽度为8
      外层空心圆盘与时针刻度之间的距离也为20
      
   4.分针刻度
      宽度为4
      长度为3
      
   5.时针
      宽度为14
      圆心外溢出80 收20
      
   6.分针
      宽度为10
      圆心外溢出112 收28
      
   7.秒针
      颜色:D40000
      宽度为6
      圆心外溢出83 收30
      
      ---->中心实心圆盘
         半径为10
      ---->秒针头
         96码开外半径为10的空心圆
         宽度为6
      
      
   
```

```javascript
//页面加载
  window.onload = function () {
    //获取画布和绘制对象
    var canvas = document.querySelector("#test");
    if (!canvas.getContext) return;
    var ctx = canvas.getContext("2d");

    setInterval(function () {
      ctx.clearRect(0,0,canvas.width,canvas.height);
      draw();
    },1000);
    draw();

    function draw() {
      //设置默认的样式

      ctx.save();
      ctx.lineWidth = 8;
      ctx.strokeStyle = "black";
      ctx.lineCap = "round";
      //移动原点,旋转到12点的方向
      ctx.translate(300, 300);
      ctx.rotate(-90 * Math.PI / 180);
      ctx.beginPath();

      //外部的空闲圆盘
      ctx.save();
      //设置圆盘的线的宽度为14
      ctx.lineWidth = 14;
      //设置圆盘的线的颜色
      ctx.strokeStyle = "green";
      ctx.beginPath();
      ctx.arc(0, 0, 140, 0, 360 * Math.PI / 180);
      ctx.stroke();
      ctx.restore();
      //时针的刻度
      ctx.save();
      for (var i = 0; i < 12; i++) {
        ctx.rotate(30 * Math.PI / 180);
        ctx.beginPath();
        ctx.moveTo(100, 0);
        ctx.lineTo(120, 0);
        ctx.stroke();
      }
      ctx.restore();

      //分针的刻度
      ctx.save();
      ctx.strokeStyle = "orange";
      ctx.lineWidth=4
      for (var i = 0; i < 60; i++) {
        //5分钟,10分钟,15分钟...的位置不需要画了
        if (i % 5 != 0) {
          ctx.beginPath();
          ctx.moveTo(117, 0);
          ctx.lineTo(120, 0);
          ctx.stroke();
        }
        ctx.rotate(6 * Math.PI / 180);
      }
      ctx.restore();

      //时针,分针,秒针,表座
      //先获取时间
      var date = new Date();
      var s = date.getSeconds();
      var m = date.getMinutes() + s / 60;
      var h = date.getHours() + m / 60;
      h = h > 12 ? h - 12 : h;//12小时制

      //绘制时针
      ctx.save();
      ctx.lineWidth = 14;//时针的粗细
      ctx.strokeStyle = "blue";
      //一小时走30度
      ctx.rotate(h * 30 * Math.PI / 180);
      ctx.beginPath();
      ctx.moveTo(-20, 0);
      ctx.lineTo(80, 0);
      ctx.stroke();
      ctx.restore();

      //绘制分针
      ctx.save();
      ctx.lineWidth = 10;//时针的粗细
      ctx.strokeStyle = "green";
      //一分钟走6度
      ctx.rotate(m * 6 * Math.PI / 180);
      ctx.beginPath();
      ctx.moveTo(-28, 0);
      ctx.lineTo(112, 0);
      ctx.stroke();
      ctx.restore();

      //绘制秒针
      ctx.save();
      ctx.lineWidth = 6;//时针的粗细
      ctx.strokeStyle = "#D40000";
      ctx.fillStyle = "#D40000";
      //一分钟走6度
      ctx.rotate(s * 6 * Math.PI / 180);
      ctx.beginPath();
      ctx.moveTo(-30, 0);
      ctx.lineTo(83, 0);
      ctx.stroke();
      //针尖和表座
      ctx.beginPath();
      ctx.arc(0, 0, 10, 0, 360 * Math.PI / 180);
      ctx.fill();
      ctx.beginPath();
      ctx.arc(96, 0, 10, 0, 360 * Math.PI / 180);
      ctx.stroke();

      ctx.restore();
      ctx.restore();
    }


  };
```

