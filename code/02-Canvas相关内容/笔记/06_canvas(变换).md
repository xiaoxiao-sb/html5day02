###canvas中的变换
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

	### 绘制图片

### 绘制图像效果

在**CanvasRenderingContext2D** 中提供了一个可以绘制图像并设置图像显示效果的方法:

**createPattern() **

参数1:要绘制的图片对象

参数2:展示的效果,参数2的值如下

- `"repeat"` (both directions),
- `"repeat-x"` (horizontal only),
- `"repeat-y"` (vertical only), 
- `"no-repeat"` (neither).

### 径向渐变

### 线性渐变

