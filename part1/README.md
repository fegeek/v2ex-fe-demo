#以v2ex为例深入学习前端开发 基础布局
![](https://raw.githubusercontent.com/fegeek/v2ex-fe-demo/master/files/v2ex-homepage-layout.png)
##布局分析
上图是v2ex首页截图，我已经用线框进行了标示，每一个不同颜色的框都是一个容器，从最外层开始分别是：头部、主体、底部三大块。所以，在这个首页的HTML页面里，肯定要有这么三个DIV。<br>

本篇先从头部入手，头部的大容器内有分成了左(Logo)、中(搜索框)、右(导航菜单)这三个部分。所以，头部的div容器我们可以先这样写一个大的布局：<br>

```Html
	<div class="container">
    	<div class="site-header-logo">
			Left
        </div>
        <div class="site-header-search">
			Center
        </div>
        <div class="site-header-menu">
			Right
        </div>
    </div>
```

上面的代码片段就是我们最原始的布局，有了这个之后，头部区域的布局也就基本确定了。<br>

再来分析一下头部的效果图。<br>

通栏背景色块、主体部分固定宽度且居中。在上面的代码片段中，我们只需对.container设置固定宽度和margin:auto; 即可实现居中并固定宽度。但是不要忘记了，顶部还有一个通栏背景色块。如何解决这个问题呢？<br>

解决办法有两个，第一个是对body设置一个背景图，让其处于水平位置平铺。另一种方法就是再定义一个外层容器，宽度为100%，然后对这个容器进行样式控制。本例中采用第二种，所以经过改进后，上面的代码片段就变成如下这样：<br>

```html
<div class="site-header">
	<div class="container">
    	<div class="site-header-logo">
			Left
        </div>
        <div class="site-header-search">
			Center
        </div>
        <div class="site-header-menu">
			Right
        </div>
    </div>
</div>
```

##样式控制
在前面的代码中，一共出现了5个Class Name：site-header container site-header-logo site-header-search site-header-menu<br>

新建一个style.css文档，定义这些class的样式。<br>

```CSS
.container{
	width:970px;
	height:auto;
	margin:auto;
}

/**
 * Site Header
 */
.site-header{
	width: 100%;
	height: 44px;
	overflow: hidden;
	background-image: url(../img/site-header-bg-repeat.png);
	background-repeat: repeat;
	background: -webkit-linear-gradient(#6ea3d9,#467aae); /* Chrome & Safari: -webkit- */
	background:    -moz-linear-gradient(#6ea3d9,#467aae); /* Firefox: -moz- */
	background:      -o-linear-gradient(#6ea3d9,#467aae); /* Opera: -o- */
	background:     -ms-linear-gradient(#6ea3d9,#467aae); /* IE: -ms- */
	background:         linear-gradient(#6ea3d9,#467aae); /* Default */
	box-shadow: 0 2px 5px 0 rgba(0,0,0,.4);
}
.site-header-logo{
	width:150px;
	height:34px;
	float:left;
	padding:5px 0;
}

.site-header-search{
	width:260px;
	height:24px;
	float:left;
	padding:10px 0;
	margin-left:20px;
}

.site-header-menu{
	float:right;
	height:24px;
	padding:10px 0;
}
```
##填入内容
容器搞定了，接下来便要开始写里面的内容了。从左边开始，我们知道，那是个Logo，鼠标点击可以回到首页。由此可知，左边这个区域里的内容就是一个带了链接的图片。<br>
```html
<a href="url" title="title"><img src="ImgUrl" alt="ImgDescription"></a>
```
再到中间区域，这是一个搜索框，再直白一点就是一个type="text"的input，所以这样写就可以了。<br>
```html
<input type="text" placeholder="Search here...">
```
最右为导航菜单，本质上就是一组链接。拆分一下，首先是“一组”，字面意义告诉我们这是N个条目，然后是“链接”，首先想到了a标签。这样简单分析之后，这部分内容就可以这么写了。<br>
```html
<ul>
	<li><a href="#">Home</a></li>
	<li><a href="#">Log In</a></li>
	<li><a href="#">Create New Account</a></li>
</ul>
```
分别置入对应的区块容器，所以头部完整的HTML代码也就出来了。
```html
<div class="site-header">
	<div class="container">
    	<div class="site-header-logo">
        	<a href="#"><img src="img/logo-header.png"></a>
        </div>
        <div class="site-header-search">
        	<input type="text" placeholder="Search here...">
        </div>
        <div class="site-header-menu">
        	<ul>
            	<li><a href="#">Home</a></li>
            	<li><a href="#">Log In</a></li>
            	<li><a href="#">Create New Account</a></li>
            </ul>
        </div>
    </div>
</div>
```
```css
.container{
	/**
	 * 定义一个共用的容器，宽度为970px
	 * 为什么要定义970？因为v2ex是970px
	 * 这个container有什么作用？
	 * 最直接的作用就是不需要为每个大区块再定义宽度
	 * 另一个作用就是为了方便后续的网页自适应开发
	 */
	width:970px;
	height:auto;
	margin:auto;/* 这句的作用是使得这个容器居中，即左右边距相等 */
}

/**
 * Site Header
 */
.site-header{
	width: 100%; /* 全屏宽度 */
	height: 44px; /* Why 44px? 因为v2ex是44px */
	overflow: hidden;
	background-image: url(../img/site-header-bg-repeat.png); /* 这句和下句主要针对旧版本浏览器，比如IE8- */
	background-repeat: repeat;
	/*
	 * 以下是通过CSS设置background渐变色
	 * 为了兼容各版本浏览器，加上各厂商的私有前缀
	 * 最新版本的浏览器均支持css3，所以无需这么繁琐
	 */
	background: -webkit-linear-gradient(#6ea3d9,#467aae); /* Chrome & Safari: -webkit- */
	background:    -moz-linear-gradient(#6ea3d9,#467aae); /* Firefox: -moz- */
	background:      -o-linear-gradient(#6ea3d9,#467aae); /* Opera: -o- */
	background:     -ms-linear-gradient(#6ea3d9,#467aae); /* IE: -ms- */
	background:         linear-gradient(#6ea3d9,#467aae); /* Default */
	box-shadow: 0 2px 5px 0 rgba(0,0,0,.4); /* box-shadow是css3的新属性，用于设置box的阴影 */
}
.site-header-logo{
	width:150px;
	height:34px;
	float:left;
	padding:5px 0;
}
.site-header-logo img{
	height:34px;
}
.site-header-search{
	width:260px;
	height:24px;
	float:left;
	padding:10px 0;
	margin-left:20px;
}
.site-header-search input[type="text"]{
	width:200px;
	height:24px;
	padding:3px 12px 3px 24px;
	border:0;
	border-radius:12px;
	background:#fff url(../img/icon-search.png) 5px center no-repeat;
}
.site-header-search input[type="text"]:focus{
	outline:none; /* 去除焦点边框 */
}
.site-header-menu{
	float:right;
	height:24px;
	padding:10px 0;
}
.site-header-menu ul{
	line-height:24px;
}
.site-header-menu ul li{
	float:left;
	margin-left:20px;
}
.site-header-menu ul li a{
	color:#fff;
	text-decoration:none;
}
.site-header-menu ul li a:hover{
	text-decoration:underline;
}
```
##一些必须了解的知识

###CSS Reset
各厂商都有自带的默认样式，而Reset的作用就是清除这些差异，然后再重新定义。比如padding、margin、border等等。<br>
###自闭合标签
HTML5认为自闭合标签无需添加/
###样式属性的先后顺序
位置、大小、浮动、边距、排版、外观<br>
非强制要求，按照个人的习惯书写即可。
###Class命名
在小型项目中，class命名规范不是很重要，但养成良好的命名习惯是很有用的，尤其是一个多人维护的项目。<br>
我的一些习惯：<br>
<ul>
<li>class全小写</li>
<li>使用中划线-连接</li>
<li>使用有意义的名称</li>
<li>尽量英文命名，汉语拼音总觉得很别扭</li>
<li>用父级容器的class作为前缀</li>
<li>赶项目的情况写，上面几点都是浮云</li>
</ul>
###代码缩进
使用tab键，而不是直接敲空格
###更多代码书写规范请参考
这篇内容非常好，推荐一看。
<a href="http://alloyteam.github.io/code-guide/" target="_blank">Code Guide by @AlloyTeam</a>