---
layout: post
title:  "Front-End Technolog"
date:   2015-12-25 13:35:30
categories: allen.hu update
---

# Front-End

[Regular-UI](https://github.com/regular-ui/regular-ui)

[MCSS](https://github.com/leeluolee/mcss)

# MASS

[mass](https://github.com/leeluolee/mass) a css toolbox based on mcss.

1. css3.mcss(源码) —— 提供海量的css3的兼容处理(由于mcss的强大特性，其实没写多少代码)
2. reset.mcss(源码) —— 提供多种reset函数, nec-reset, normalize ... etc
3. helper.mcss(源码) —— 提供一些常用帮助函数，比如$clearfix等等
4. layout.mcss(源码) —— 提供一些布局相关函数
5. effect.mcss(源码) —— 提供一些常用的animation mixin, 并提供参数控制.
6. functions.mcss(源码) —— 一些函数集合, mass的每个文件都或多或少依赖了这个函数
7. var.mcss(源码) —— 全局变量, 目前只有两个
8. index.mcss(源码) —— 以上所有子文件的入口文件, 你偷懒可以只引入这个文件
需要注意的是 : mass中的所有文件都可以单独引入, 已经处理好了依赖关系。

* 同名 vendor prefixr:

```
Example

.u-btn{
  /* 注意mcss同时支持两种函数调用方式 */
  $transition: background-color 0.1s ease-in-out;
  $box-sizing(border-box)
}
Outport

.u-btn{
  -webkit-transition:background-color 0.1s ease-in-out;
  -moz-transition:background-color 0.1s ease-in-out;
  transition:background-color 0.1s ease-in-out;
  -webkit-box-sizing:border-box;
  -moz-box-sizing:border-box;
  box-sizing:border-box;
}

# w3school

[w3school](http://www.w3school.com.cn/css/index.asp)

## CSS

### CSS简介

一般而言，所有的样式会根据下面的规则层叠于一个新的虚拟样式表中，其中数字 4 拥有最高的优先权。
浏览器缺省设置
外部样式表
内部样式表（位于 <head> 标签内部）
内联样式（在 HTML 元素内部）
因此，内联样式（在 HTML 元素内部）拥有最高的优先权，这意味着它将优先于以下的样式声明：<head> 标签中的样式声明，外部样式表中的样式声明，或者浏览器中的样式声明（缺省值）。

### CSS语法基础

CSS 规则由两个主要的部分构成：选择器，以及一条或多条声明。
selector {declaration1; declaration2; ... declarationN }

body {
  color: #000;
  background: #fff;
  margin: 0;
  padding: 0;
  font-family: Georgia, Palatino, serif;
  }

### CSS高级语法
选择器的分组
继承问题

### CSS派生选择器

比方说，你希望列表中的 strong 元素变为斜体字，而不是通常的粗体字，可以这样定义一个派生选择器：
li strong {
    font-style: italic;
    font-weight: normal;
  }

### ID选择器

div#sidebar {
	border: 1px dotted #000;
	padding: 10px;
	}

### CSS类选择器

CSS 中，类选择器以一个点号显示：
.center {text-align: center}

### 属性选择器

input[type="text"]
{
  width:150px;
  display:block;
  margin-bottom:10px;
  background-color:yellow;
  font-family: Verdana, Arial;
}

input[type="button"]
{
  width:120px;
  margin-left:35px;
  display:block;
  font-family: Verdana, Arial;
}

### CSS背景

背景色

p {background-color: gray; padding: 20px;}

背景图像

body {background-image: url(/i/eg_bg_04.gif);}

背景定位

body
  {
    background-image:url('/i/eg_bg_03.gif');
    background-repeat:no-repeat;
    background-position:center;
  }

### CSS 文本

缩进文本

p {text-indent: 5em;}


文本对齐

text-align

字间隔

word-spacing

### CSS字体

指定字体系列

body {font-family: sans-serif;}


字体风格

font-style

字体加粗

font-weight

字体大小

font-size


### CSS链接

a:link {color:#FF0000;}		/* 未被访问的链接 */
a:visited {color:#00FF00;}	/* 已被访问的链接 */
a:hover {color:#FF00FF;}	/* 鼠标指针移动到链接上 */
a:active {color:#0000FF;}	/* 正在被点击的链接 */

### CSS列表

列表类型

ul {list-style-type : square}


列表顶图像

ul li {list-style-image : url(xxx.gif)}


### CSS 表格

折叠边框

table
  {
  border-collapse:collapse;
  }

table,th, td
  {
  border: 1px solid black;
  }

表格宽度, 高度

表格文本对齐

### CSS轮廓

outline	在一个声明中设置所有的轮廓属性。	2
outline-color	设置轮廓的颜色。	2
outline-style	设置轮廓的样式。	2
outline-width	设置轮廓的宽度。

### CSS框模型概述

![boxmodle](../../images/boxmodel.png)

元素框的最内部分是实际的内容，直接包围内容的是内边距。内边距呈现了元素的背景。内边距的边缘是边框。边框以外是外边距，外边距默认是透明的，因此不会遮挡其后的任何元素。

1. 背景应用于由内容和内边距、边框组成的区域。
2. 在 CSS 中，width 和 height 指的是内容区域的宽度和高度。增加内边距、边框和外边距不会影响内容区域的尺寸，但是会增加元素框的总尺寸。
3. 提示：内边距、边框和外边距可以应用于一个元素的所有边，也可以应用于单独的边。
4. 提示：外边距可以是负值，而且在很多情况下都要使用负值的外边距。

### CSS内边距

单边内边距属性
也通过使用下面四个单独的属性，分别设置上、右、下、左内边距：
padding-top
padding-right
padding-bottom
padding-left


h1 {
  padding-top: 10px;
  padding-right: 0.25em;
  padding-bottom: 2ex;
  padding-left: 20%;
  }

内边距的百分比数值
前面提到过，可以为元素的内边距设置百分数值。百分数值是相对于其父元素的 width 计算的，这一点与外边距一样。所以，如果父元素的 width 改变，它们也会改变。

### CSS边框

边框与背景

边框的样式

边框的宽度

没有边框
p {border-style: none; border-width: 50px;}

边框的颜色

p {
  border-style: solid;
  border-color: blue rgb(25%,35%,45%) #909090 red;
  }

透明边框

a:link, a:visited {
  border-style: solid;
  border-width: 5px;
  border-color: transparent;
  }

### CSS外边距

如果缺少左外边距的值，则使用右外边距的值。
如果缺少下外边距的值，则使用上外边距的值。
如果缺少右外边距的值，则使用上外边距的值。

### CSS外边距合并
,
外边距合并指的是，当两个垂直外边距相遇时，它们将形成一个外边距。
合并后的外边距的高度等于两个发生合并的外边距的高度中的较大者。

外边距合并指的是，当两个垂直外边距相遇时，它们将形成一个外边距。
合并后的外边距的高度等于两个发生合并的外边距的高度中的较大者。

### CSS定位

CSS定位与浮动

CSS 为定位和浮动提供了一些属性，利用这些属性，可以建立列式布局，将布局的一部分与另一部分重叠，还可以完成多年来通常需要使用多个表格才能完成的任务。
定位的基本思想很简单，它允许你定义元素框相对于其正常位置应该出现的位置，或者相对于父元素、另一个元素甚至浏览器窗口本身的位置。显然，这个功能非常强大，也很让人吃惊。要知道，用户代理对 CSS2 中定位的支持远胜于对其它方面的支持，对此不应感到奇怪。

一切皆为框

div、h1 或 p 元素常常被称为块级元素。这意味着这些元素显示为一块内容，即“块框”。与之相反，span 和 strong 等元素称为“行内元素”，这是因为它们的内容显示在行中，即“行内框”。
您可以使用 display 属性改变生成的框的类型。这意味着，通过将 display 属性设置为 block，可以让行内元素（比如 <a> 元素）表现得像块级元素一样。还可以通过把 display 设置为 none，让生成的元素根本没有框。这样的话，该框及其所有内容就不再显示，不占用文档中的空间。
但是在一种情况下，即使没有进行显式定义，也会创建块级元素。这种情况发生在把一些文本添加到一个块级元素（比如 div）的开头。即使没有把这些文本定义为段落，它也会被当作段落对待：

<div>
some text
<p>Some more text.</p>
</div>

CSS 实位机制
CSS 有三种基本的定位机制：普通流、浮动和绝对定位。
除非专门指定，否则所有框都在普通流中定位。也就是说，普通流中的元素的位置由元素在 (X)HTML 中的位置决定。
块级框从上到下一个接一个地排列，框之间的垂直距离是由框的垂直外边距计算出来。
行内框在一行中水平布置。可以使用水平内边距、边框和外边距调整它们的间距。但是，垂直内边距、边框和外边距不影响行内框的高度。由一行形成的水平框称为行框（Line Box），行框的高度总是足以容纳它包含的所有行内框。不过，设置行高可以增加这个框的高度。


CSS Positon属性

static
元素框正常生成。块级元素生成一个矩形框，作为文档流的一部分，行内元素则会创建一个或多个行框，置于其父元素中。

relative
元素框偏移某个距离。元素仍保持其未定位前的形状，它原本所占的空间仍保留。

absolute
元素框从文档流完全删除，并相对于其包含块定位。包含块可能是文档中的另一个元素或者是初始包含块。元素原先在正常文档流中所占的空间会关闭，就好像元素原来不存在一样。元素定位后生成一个块级框，而不论原来它在正常流中生成何种类型的框。

fixed
元素框的表现类似于将 position 设置为 absolute，不过其包含块是视窗本身。

overflow: scroll
overflow: hidden
overflow: auto

Z-index
Z-index可被用于将在一个元素放置于另一元素之后。


### CSS相对定位

相对定位是一个非常容易掌握的概念。如果对一个元素进行相对定位，它将出现在它所在的位置上。然后，可以通过设置垂直或水平位置，让这个元素“相对于”它的起点进行移动。


![relative position]('../../images/relative.png')


### 绝对定位

设置为绝对定位的元素框从文档流完全删除，并相对于其包含块定位，包含块可能是文档中的另一个元素或者是初始包含块。元素原先在正常文档流中所占的空间会关闭，就好像该元素原来不存在一样。元素定位后生成一个块级框，而不论原来它在正常流中生成何种类型的框。


绝对定位的元素的位置相对于最近的已定位祖先元素，如果元素没有已定位的祖先元素，那么它的位置相对于最初的包含块。
对于定位的主要问题是要记住每种定位的意义。所以，现在让我们复习一下学过的知识吧：相对定位是“相对于”元素在文档中的初始位置，而绝对定位是“相对于”最近的已定位祖先元素，如果不存在已定位的祖先元素，那么“相对于”最初的包含块。
注释：根据用户代理的不同，最初的包含块可能是画布或 HTML 元素。

![absolute position]('../../images/absolute.png')

### CSS 浮动

浮动的框可以向左或向右移动，直到它的外边缘碰到包含框或另一个浮动框的边框为止。
由于浮动框不在文档的普通流中，所以文档的普通流中的块框表现得就像浮动框不存在一样。


要想阻止行框围绕浮动框，需要对该框应用 clear 属性。clear 属性的值可以是 left、right、both 或 none，它表示框的哪些边不应该挨着浮动框。

![clear]('../../images/clear.png')

这样可以实现我们希望的效果，但是需要添加多余的代码。常常有元素可以应用 clear，但是有时候不得不为了进行布局而添加无意义的标记。
不过我们还有另一种办法，那就是对容器 div 进行浮动：
.news {
  background-color: gray;
  border: solid 1px black;
  float: left;
  }

.news img {
  float: left;
  }

.news p {
  float: right;
  }

<div class="news">
<img src="news-pic.jpg" />
<p>some text</p>
</div>
这样会得到我们希望的效果。不幸的是，下一个元素会受到这个浮动元素的影响。为了解决这个问题，有些人选择对布局中的所有东西进行浮动，然后使用适当的有意义的元素（常常是站点的页脚）对这些浮动进行清理。这有助于减少或消除不必要的标记。
事实上，W3School 站点上的所有页面都采用了这种技术，如果您打开我们使用 CSS 文件，您会看到我们对页脚的 div 进行了清理，而页脚上面的三个 div 都向左浮动。


### CSS元素选择器(类型选择器)

### CSS选择器分组

### CSS类选择器

.important {color:red;}

p.important {color:red;}

多类选择器

<p class="important warning">

### CSS ID选择器

#intro {font-weight:bold;}

<p id="intro">This is a paragraph of introduction.</p>

### CSS 属性选择器

如果您希望把包含标题（title）的所有元素变为红色，可以写作：
*[title] {color:red;}


可以只对有 href 属性的锚（a 元素）应用样式：
a[href] {color:red;}

### CSS 后代选择器

后代选择器（descendant selector）又称为包含选择器。
后代选择器可以选择作为某元素后代的元素。

有关后代选择器有一个易被忽视的方面，即两个元素之间的层次间隔可以是无限的。

div.sidebar {background:blue;}
div.maincontent {background:white;}
div.sidebar a:link {color:white;}
div.maincontent a:link {color:blue;}

h1 em {color:red;}

<h1>This is a <em>important</em> heading</h1>

### CSS 子元素选择器

与后代选择器相比，子元素选择器（Child selectors）只能选择作为某元素子元素的元素。

如果您希望选择只作为 h1 元素子元素的 strong 元素，可以这样写：
h1 > strong {color:red;}


结合后代选择器和子选择器
请看下面这个选择器：
table.company td > p
上面的选择器会选择作为 td 元素子元素的所有 p 元素，这个 td 元素本身从 table 元素继承，该 table 元素有一个包含 company 的 class 属性。

### CSS 相邻兄弟选择器

h1 + p {margin-top:50px;}
这个选择器读作：“选择紧接在 h1 元素后出现的段落，h1 和 p 元素拥有共同的父元素”。

### CSS 伪类选择器

a:link {color: #FF0000}		/* 未访问的链接 */
a:visited {color: #00FF00}	/* 已访问的链接 */
a:hover {color: #FF00FF}	/* 鼠标移动到链接上 */
a:active {color: #0000FF}	/* 选定的链接 */


### CSS 伪元素

"first-line" 伪元素用于向文本的首行设置特殊样式。

注释："first-line" 伪元素只能用于块级元素。
注释：下面的属性可应用于 "first-line" 伪元素：
font
color
background
word-spacing
letter-spacing
text-decoration
vertical-align
text-transform
line-height
clear


:first-letter 伪元素
"first-letter" 伪元素用于向文本的首字母设置特殊样式：

CSS2 - :before 伪元素
":before" 伪元素可以在元素的内容前面插入新内容。
下面的例子在每个 <h1> 元素前面插入一幅图片：
h1:before
  {
  content:url(logo.gif);
  }

CSS2 - :before 伪元素
":before" 伪元素可以在元素的内容前面插入新内容。
下面的例子在每个 <h1> 元素前面插入一幅图片：
h1:before
  {
  content:url(logo.gif);
  }
亲自试一试
CSS2 - :after 伪元素
":after" 伪元素可以在元素的内容之后插入新内容。
下面的例子在每个 <h1> 元素后面插入一幅图片：
h1:after
  {
  content:url(logo.gif);
  }

.m-progress:after{
content:'';
clear: both;
display:block;
}

.m-progress{
overflow:hidden
}

BFC技巧

background: 用于样式
img: 用于图片

居中:
text-aliign: center
line-height: 父元高度()

ul:
text-align: center
li: display: inline-block

居中
width:990px;
margin: 0 auto

body: background

宽度优先,高度不管

绝对定位基本不用

### CSS 水平对齐

对齐块元素
块元素指的是占据全部可用宽度的元素，并且在其前后都会换行。

```
.center
{
margin-left:auto;
margin-right:auto;
width:70%;
background-color:#b0e0e6;
}

如果宽度是100%,对齐没有效果

```
使用 position 属性进行左和右对齐
对齐元素的方法之一是使用绝对定位：
实例
.right
{
position:absolute;
right:0px;
width:300px;
background-color:#b0e0e6;
}

注释：绝对定位元素会被从正常流中删除，并且能够交叠元素。


使用 float 属性来进行左和右对齐
对齐元素的另一种方法是使用 float 属性：
实例
.right
{
float:right;
width:300px;
background-color:#b0e0e6;
}

### 三个定位方案

在定位的时候，浏览器就会根据元素的盒类型和上下文对这些元素进行定位，可以说盒就是定位的基本单位。定位时，有三种定位方案，分别是常规流，浮动已经绝对定位。

常规流(Normal flow)

在常规流中，盒一个接着一个排列;
在块级格式化上下文里面， 它们竖着排列；
在行内格式化上下文里面， 它们横着排列;
当position为static或relative，并且float为none时会触发常规流；
对于静态定位(static positioning)，position: static，盒的位置是常规流布局里的位置；
对于相对定位(relative positioning)，position: relative，盒偏移位置由这些属性定义top，bottom，leftandright。即使有偏移，仍然保留原有的位置，其它常规流不能占用这个位置。

浮动(Floats)

盒称为浮动盒(floating boxes)；
它位于当前行的开头或末尾；
这导致常规流环绕在它的周边，除非设置 clear 属性；


绝对定位(Absolute positioning)

绝对定位方案，盒从常规流中被移除，不影响常规流的布局；
它的定位相对于它的包含块，相关CSS属性：top，bottom，left及right；
如果元素的属性position为absolute或fixed，它是绝对定位元素；
对于position: absolute，元素定位将相对于最近的一个relative、fixed或absolute的父元素，如果没有则相对于body；


最常见的就是overflow:hidden、float:left/right、position:absolute。也就是说，每次看到这些属性的时候，就代表了该元素以及创建了一个BFC了。

position:static的时候, left 属性没有用的


### CSS尺寸

height
line-height
max-height
max-width
min-height
min-width
width

inline, inline-block, block , none




## HTML

 块元素

 块级元素占一行，不论内容多少只要是有2个这样的元素就会换行，行内元素内容少时不会换行。这是个重要区别。

 块级元素(block element)
 div -最常用的块级元素
 dl - 和dt dd搭配使用的块级元素
 form - 交互表单
 h1 - 大标题
 hr - 水平分隔线
 ol - 排序表单`
 p - 段落
 ul - 非排序列表
 li - 定义列表项


 内联元素(inline element)
 a - 锚点
 b - 粗体(不推荐)
 br - 换行
 em - 强调
 font - 字体设定(不推荐)
 i - 斜体
 img - 图片
 input - 输入框
 label - 表格标签
 select - 项目选择
 small - 小字体文本
 span - 常用内联容器，定义文本内区块
 strike - 中划线
 strong - 粗体强调
 sub - 下标
 sup - 上标
 textarea - 多行文本输入框
 tt - 电传文本
 u - 下划线

 #ICP前端开发框架总结

## HTML
    Emnet
## CSS
   LESS,MCSS
## JavaScript
  React.js  React native
src/forms
   /net
   /cache
   /protocol(encoder,decorder),(front and end data interface, interface api for other service)
   /utils(globalsManager, validator(form datum validate))
   /constant
   /widgets（ant.design, react-ui, material-ui）
 ## webpack



