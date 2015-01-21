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

