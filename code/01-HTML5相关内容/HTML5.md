## HTML5

概述:HTML5是HTML最新的修订版本，2014年10月由万维网联盟（W3C）完成标准制定。

HTML5的设计目的是为了在移动设备上支持多媒体。

总结:HTML5就是HTML4的一个升级(加入了新的语义化标签和语义化的属性及新的表单控件)

### HTML5中的新特性

- 用于绘画的 canvas 元素
- 用于媒介回放的 video 和 audio 元素
- 对本地离线存储的更好的支持
- 新的特殊内容元素，比如 article、footer、header、nav、section
- 新的表单控件，比如 calendar、date、time、email、url、search



### HTML5的改进

- 新元素
- 新属性
- 完全支持 CSS3
- Video 和 Audio
- 2D/3D 制图
- 本地存储
- 本地 SQL 数据
- Web 应用



### HTML的优势

跨平台:PC和移动端全部都支持---提高用户体验

网页的功能扩展:不需要下载客户端或者插件就可以看视频,玩游戏,或者操作更加简单

降低成本:开发者针对不同的操作系统开发,都需要自己研究,现在不需要了,一次开发多次使用,可以直接封装非app---时间和资金成本全部降低---跨系统移植

搜索引擎优化:HTML5新增的标签，使搜索引擎更加容易抓取和索引网页，从而驱动网站获得更多的点击流量。





### HTML中的语义元素

语义化标签:

| 标签        | 描述                         |
| --------- | -------------------------- |
| <header>  | 定义了文档的头部区域                 |
| <footer>  | 定义 section 或 document 的页脚。 |
| <nav>     | 定义导航链接的部分。                 |
| <article> | 定义页面独立的内容区域。               |
| <aside>   | 定义页面的侧边栏内容。                |
| <section> | 定义文档中的节（section、区段）。       |
| <hgroup>  | 群组标题                       |

语义化的好处:HTML5可以让很多更语义化结构化的代码标签代替大量的无意义的div标签这种语义化的特性提升了网页的质量和语义对搜索引擎更加的友好

注意:

```html
hgroup元素代表 网页 或 section 的标题进行组合，当元素有多个层级时，该元素可以将h1到h6元素放在其内，譬如文章的主标题和副标题的组合
	
		<hgroup>
		    <h1>HTML 5</h1>
		    <h2>这是一篇介绍HTML 5语义化标签和更简洁的结构</h2>
		</hgroup>
	
hgroup使用注意：
			如果只需要一个h1-h6标签就不用hgroup
			如果有连续多个h1-h6标签就用hgroup
			如果有连续多个标题和其他文章数据，h1-h6标签就用hgroup包住，和其他文章元数据一起放入header标签
```

```html
	header 元素代表 网页 或 section 的页眉。
		通常包含h1-h6元素或hgroup
	
		<header>
		    <hgroup>
		        <h1>网站标题</h1>
		        <h2>网站副标题</h2>
		    </hgroup>
		</header>
		
		header使用注意：
			可以是“网页”或任意“section”的头部部分
			没有个数限制。
			如果hgroup或h1-h6自己就能工作的很好，那就不要用header。
```

```html
	nav元素代表页面的导航链接区域。用于定义页面的主要导航部分。
	
		<nav>
		    <ul>
		        <li>HTML 5</li>
		        <li>CSS3</li>
		        <li>JavaScript</li>
		    </ul>
		</nav>
		
		nav使用注意：
			用在整个页面主要导航部分上，不合适就不要用nav元素；
```

```html
	section元素代表文档中的 节 或 段，段可以是指一篇文章里按照主题的分段；节可以是指一个页面里的分组。
	
		<section>
		    <h1>section是啥？</h1>
		    <article>
		        <h2>关于section</h1>
		        <p>section的介绍</p>
		        <section>
		            <h3>关于其他</h3>
		            <p>关于其他section的介绍</p>
		        </section>
		    </article>
		</section>
		
		section使用注意：
			section不是一般意义上的容器元素，如果想作为样式展示和脚本的便利，可以用div。
			article、nav、aside可以理解为特殊的section，
			所以如果可以用article、nav、aside就不要用section，没实际意义的就用div	
```

```html
	article元素最容易跟section和div容易混淆，其实article代表一个在文档，页面或者网站中自成一体的内容
	
		<article>
		    <h1>一篇文章</h1>
		    <p>文章内容..</p>
		    <footer>
		        <p><small>版权：html5jscss网所属，作者：damu</small></p>
		    </footer>
		</article>
		
		article使用注意：
			独立文章：用article
			单独的模块：用section
			没有语义的：用div
```

```html
aside元素被包含在article元素中作为主要内容的附属信息部分，其中的内容可以是与当前文章有关的相关资料、标签、名次解释等
		
		在article元素之外使用作为页面或站点全局的附属信息部分。最典型的是侧边栏，其中的内容可以是日志串连，其他组的导航，甚至广告，这些内容相关的页面。
		
		<article>
		    <p>内容</p>
		    <aside>
		        <h1>作者简介</h1>
		        <p>小北，前端一枚</p>
		    </aside>
		</article>
		
		aside使用总结：
			aside在article内表示主要内容的附属信息，
			在article之外则可做侧边栏
			如果是广告，其他日志链接或者其他分类导航也可以用
```

```html
	footer元素代表 网页 或 section 的页脚，通常含有该节的一些基本信息，譬如：作者，相关文档链接，版权资料。
	
		<footer>
		    COPYRIGHT@damu
		</footer>
		
		footer使用注意：
			可以是 网页 或任意 section 的底部部分；
			没有个数限制，除了包裹的内容不一样，其他跟header类似。
```





### HTML5标签演示

```html
<header>
		<hgroup>
			<h1>我是header</h1>
			<h2>我是header的副标题</h2>
		</hgroup>
	</header><!-- /header -->
	<section>
		<header>
			<hgroup>
				<h1>我是content</h1>
				<h2>我是content的副标题</h2>
			</hgroup>
		</header><!-- /header -->
	</section>
	<footer>
		<header>
			<hgroup>
				<h1>我是footer</h1>
				<h2>我是footer的副标题</h2>
			</hgroup>
		</header><!-- /header -->
	</footer>
```

检测网址:https://gsnedders.html5.org/outliner/

### HTML5中新增的DOM操作介绍

1.获取元素的方式:

```javascript
document.querySelector("选择器");单个的
```

```
document.querySelectorAll("选择器");多个的
```

```javascript
divObj.classList 返回的是一个存放了所有类样式名字的数组
.add()添加类样式
.remove()删除类样式
.toggle()切换类样式
.contains()是否包含某个类样式
```



### HTML5中自定义属性的操作

```html
<div id="dv" name="小黑" data-des="真黑啊" data-sex="男"></div>
```

```javascript
//HTML5中新增加了一个关于自定义属性的数据集:dataset--统一写法,方便操作
对象.dataset---->获取的是所有自定义属性的数组
添加自定义属性: 对象.dataset.属性名字="值";
获取自定义属性: 对象.dataset.属性名;
注意自定义属性名字如果是多个单词组合该如何添加?(驼峰命名法即可)
对象.dataset.myFace="值";最终在html标签上就可以看到:data-my-face="值";
可以使用键值的方式来设置自定义属性:
对象.dataset["属性名字"]="值";
```

### HTML5中的可编辑属性

```html
<div contenteditable="true">
  可以编辑
</div>
页面中的div可以直接进行编辑
```



### HTML5和HTML4的对比

1.写法不同:

```html
!   直接tab键---->页面中h5的html标签内容全部导入
html:4s 直接tab键--->页面中h4严格版的标签内容全部导入
还有其他的写法:html:4t等等----不介绍了
```

2.要求不同:

```html
HTML5的写法比较随意,怎么写浏览器都认识
HTML4(严格)的写法,必须要严格的写
验证的网址
https://validator.w3.org/check
```

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
<html lang="en">
<head>
  <meta http-equiv="Content-Type" content="text/html;charset=UTF-8">
  <title>Document</title>
</head>
<body>
<img src="" alt="">
</body>
</html>

HTML4的写法(严格的模式)

```

3.DOCTYPE和浏览器渲染模式

```
DOCTYPE和浏览器渲染模式
   DOCTYPE，或者称为 Document Type Declaration（文档类型声明，缩写 DTD）
   通常情况下，DOCTYPE 位于一个 HTML 文档的最前面的位置，位于根元素 HTML 的起始标签之前。
   因为浏览器必须在解析 HTML 文档正文之前就确定当前文档的类型，以决定其需要采用的渲染模式，
   不同的渲染模式会影响到浏览器对于 CSS 代码甚至 JavaScript 脚本的解析
```

```
到目前为止，各浏览器主要包含了三种模式。在 HTML5 草案中，更加明确的规定了模式的定义：
```

| 传统名称                        | HTML5草案名            | document.compatMode返回值 |
| --------------------------- | ------------------- | ---------------------- |
| standards mode(strict mode) | no-quirks mode      | CSS1Compat             |
| almost standards mode       | limited-quirks mode | CSS1Compat             |
| quirks mode                 | quirks mode         | BackCompat             |

```
document.compatMode
    document.compatMode 属性最初由微软在 IE 中创造出来，这是一个只读的属性，返回一个字符串，
    只可能存在两种返回值：
      BackCompat：标准兼容模式未开启（怪异模式）
      CSS1Compat：标准兼容模式已开启（标准模式）
在现代主流浏览器中，其实怪异模式的渲染和标准与几乎标准间没有太大的差别（ie9+ 谷歌 火狐 ...）
	    ie5.5之前都是ie自己的渲染模式，怪异模式
	    ie6才开始慢慢支持标准，标准模式，在ie6 中怪异和标准模式的区别最大
	    ie7 8 9都是基于标准模式升级的，他们理论上存在怪异模式
	
		HTML5提供的<DOCTYPE html>是标准模式，向后兼容的,等同于开启了标准模式，
		那么浏览器就得老老实实的按照W3C的 标准解析渲染页面
		一个不含任何 DOCTYPE 的网页将会以 怪异(quirks) 模式渲染。
```

**总结:写页面都要加<!DOCTYPE>**

5.根元素

H4中的根元素:<html xmlns="http://www.w3.org/1999/xhtml">可以继续用,H5中省略的

xmlns:这是XHTML1.0的东西，
   它的意思是在这个页面上的元素都位于http://www.w3.org/1999/xhtml这个命名空间内
   但是HTML5中的每个元素都具有这个命名空间，不需要在页面上再显示指出

6.head元素:

```
MIME类型:
   每当浏览器请求一个页面时，web服务器会在发送实际页面内容之前，先发送一些头信息。
   浏览器需要这些信息来决定如何解析随后的页面内容。最重要的是Content-Type
   
   比如: Content-Type:text/html
   
   text/html:即这个页面的"内容类型",或者称为MIME类型。这个头信息将唯一确定某个资源的本质是什么
   也决定了它应该如何被呈现。
   
   图片也有自己的MIME类型     
      jpg:image/jpeg   
      png:image/png
      
   js也有自己的MIME类型，css也有自己的MIME类型，
      任何资源都有自己的MIME类型，整个web都依靠MIME类型来运作
      
      
      
<meta charset="UTF-8">:
   告诉浏览器你应该使用哪种编码来解析网页
```

