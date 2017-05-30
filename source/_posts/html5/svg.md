---
title: svg图标库以及与icon font对比
date: 2016-05-10 15:02:34
categories: html5
tags: [html5,svg,icon font]
---

新版官网上线已有一段时间了，这次改版的风格是尽可能的使用图片表达，其中用到了大量的图标。
一般情况下，大量图标出现，前端直接使用 CSS Sprite即可搞定（gulp-css-spriter，这个我们留着以后再讲）。但是这次图标的使用场景有些特殊：

* 1、图标是整站统一的，会跨项目重复使用。
* 2、适配Retina屏。
* 3、同一图标根据不同的使用场景，大小，颜色会有所不同，存在颜色叠加的情况。

基于以上需求，你一定也想到了，做一套属于我们自己的矢量字体图标库是再合适不过了。那么现在问题来了，究竟是使用 SVG font 还是icon font ？为什么最终我们选择了svg font呢？
那么为什么我们要用svg font？

### 一、渲染方式

* icon font：采用的是字体渲染。icon font在一倍屏幕下渲染效果并不好，在细节部分锯齿还是很明显的（请看下图对比）。因为浏览器认为其是文本，所以会对其使用抗锯齿，尤其在火狐浏览器上的渲染比在其它浏览器上的渲染要更重些。这会让整个页面显得不好看且笨重。（即便是加henting hack，路径也会有瑕疵）。

* inline SVG：它是传统图片格式的一种，自身提供的功能集涵盖了嵌套转换、裁剪路径、Alpha通道、滤镜效果等能力，它还具备了传统图片没有的矢量功能，在任何高清设备都很高清。在浏览器中使用的是图形渲染，所以就是实实在在的路径。

<img src="https://loulanyijian.github.io/images/svg.png" alt="svg与icon font锯齿对比">
      
### 二、CSS 控制

* icon font：可以通过 CSS 控制图标大小（ 使用 font-size）， 颜色，阴影，旋转等。
* inline SVG：和 icon font 一样，可以使用同样的控制器。更赞的是，可以 
	* 1.控制图标的各个部分； 
	* 2.使用 CSS 控制 SVG 特有的属性，如描边属性。
	* 3.令人欣喜的svg动画（这个留着下次再讲）。
 
### 三、颜色支持

* icon font：只支持单色，icon font做为字体无法支持多色图形，这就对设计造成了许多限制，因此这也成为了icon font的一个瓶颈。
* inline SVG：支持单色、多色图标。这个完全满足了项目中彩色图标的使用场景，不仅可以减少代码量，更是大大减少了设计师的工作量。

### 四、定位

* icon font：定位 icon font 会是一个令人沮丧的过程。这些图标是通过伪元素插入的，它依赖于 line-height ， vertical-align，letter-spacing ， word-spacing ，字体字形设计（它的四周有留白吗？它有字距信息吗？）。如果字符有相关特效，伪元素将会显示这些特效。
* inline SVG：SVG 的显示尺寸就是它本身的尺寸

### 五、网络加载

* icon font：icon font 可能会失效，因为：
* 1. 它被跨域加载，而没有使用正确的 CORS 头信息（Firefox和IE9不支持对icon font字体的跨域访问，需要在图标字体文件所在服务器配置Header参数“Access-Control-Allow-Origin”允许当前域名才可以。而且，经过验证，必须将参数“Access-Control-Allow-Origin”配置为“*”才可以，配置为“*.当前域名”并不可以，不知道啥原因）。 
* 2. 因为任何原因，字体文件加载失败（网络抽风，服务器故障等）。
* 3. Chrome一些奇怪的漏洞会跳过 @font-face 规则，并使用 fallback 的字体取代它。
* 4.  一些浏览器不支持 @font-face。在所有的原因中，字体加载失败是最常见的（如果字体加载失败，会出现下图所示情况，这常常会让人抓狂）。

<img src="https://loulanyijian.github.io/images/svg1.jpeg">

* inline SVG：inline SVG 是在文档流中，只要浏览器支持，它就会显示（这会让我们对自己的代码更自信）。

### 六、性能

性能应该是大家最关注的为题了，为了测试的可靠性，在icomoon挑选了 491个免费ICON，分别生成了Svg图标和icon font在Chrome Timeline做了测试（测试内容分别对demo页面491图标的 Loading、Rendering、Painting这三个指标）
* 1）结果svg整体是的 **Rendering项基本上是碾压了icon font** 
上述SVG案例中我用了两种不同引用方式，一种是在页面直接inline svg方式插入的方法和用svg sprite合并后引用图标的两种，结果显示svg sprite的性能是最高的。
* 2）大批量的测试结果SVG性能已经比较有保证了，但实际项目中一个页面不可能会存在这么多图标，我们按正常页面出现图标10-30个这个区间，  取15个图标为中间值 在进行一次测试看看，结果是Rendering 的渲染结果和之前差不多，icon font所用时间依旧比svg icon要多，但是inline svg和svg sprite两种不同用法之间的差异却变得非常小，几乎 Rendering 的时间是差不多的。

### 七、语义化

* icon font：如果是正确地使用，你会通过空的伪元素来显示你的图标。 这样是否合适或者符合语意的，取决于你如何看待这类写法。
* inline SVG：`<svg>` 的语意是说“我是个图片。”——这看起来似乎好些。

### 八、无障碍（针对视觉障碍人士）

* icon font：使用 icon font 必须要非常小心，以确保做到无障碍访问。基本上，你需要做到这篇文章里所描述的。你必须一直很小心，以确保该图标本身不可朗读（但别的文本部分可读）（浏览器会认为 icon font 是「文本」从而朗读，而视觉障碍人士并不需要这些无意义的「文本」）。
* inline SVG：研究表明，使用元素的适当的组合和属性，如 <title>、<desc>和 aria-labelledby 可以很好地透过浏览器传达信息。并且，没有奇怪的故障状态。

### 九、唯一的痛点-浏览器兼容性

* icon font：很广泛。即使是 IE 6。
* inline SVG：不是特别好，不兼容 IE 8- 以及 Android 2.3-（但是我司已经英明神武的放弃了IE8及以下-此处应该有掌声）。
 以上，结合我司高大上的项目已经完全傲娇的脱离了IE 8-以及实际项目中的具体需求，在pc端中，我们果断的使用了SVG。
