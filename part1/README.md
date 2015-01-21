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
	height: 44px; /* Why 44px? 因为v2ex是44px */
	overflow: hidden;
	background-image: url(../img/site-header-bg-repeat.png);
	background-repeat: repeat;
	/*
	 * 以下是设置background渐变色
	 * 为了兼容各版本浏览器，加上各厂商的私有前缀
	 * 最新版本的浏览器均支持css3，所以无需这么繁琐
	 */
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
