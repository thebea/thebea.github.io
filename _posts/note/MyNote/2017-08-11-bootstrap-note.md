---
layout: post
title: "Bootstrap学习笔记"
date: 2017-08-11 09:00:00 +0800 
categories: 笔记
tag: MyNote
---
* content
{:toc}

`前端框架学习`。

<!-- more -->

<!-- TOC -->

- [概览](#概览)
- [栅格系统](#栅格系统)
- [排版](#排版)
- [代码](#代码)
- [表格](#表格)
- [表单](#表单)
- [按钮](#按钮)
- [图片](#图片)
- [辅助类](#辅助类)
- [响应式工具](#响应式工具)
- [使用 Less](#使用Less)
- [使用 Sass](#使用Sass)

<!-- /TOC -->

`2017-08-11`

## 概览

---

### HTML5 文档类型

Bootstrap 使用了一些 HTML5 元素和 CSS 属性。Bootstrap 项目的开头包含下面的代码段：

```html
<!DOCTYPE html>
<html>
....
</html>
```

如果在 Bootstrap 创建的网页开头不使用 HTML5 的文档类型（Doctype），您可能会面临一些浏览器显示不一致的问题，甚至可能面临一些特定情境下的不一致，以致于您的代码不能通过 W3C 标准的验证。

---

### 移动设备优先

为了让 Bootstrap 开发的网站对移动设备友好，确保适当的绘制和触屏缩放，需要在网页的 head 之中添加 viewport meta 标签，如下所示：

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

width 属性控制设备的宽度。假设您的网站将被带有不同屏幕分辨率的设备浏览，那么将它设置为 device-width 可以确保它能正确呈现在不同设备上。

initial-scale=1.0 确保网页加载时，以 1:1 的比例呈现，不会有任何的缩放。
在移动设备浏览器上，通过为 viewport meta 标签添加 user-scalable=no 可以禁用其缩放（zooming）功能。
通常情况下，maximum-scale=1.0 与 user-scalable=no 一起使用。这样禁用缩放功能后，用户只能滚动屏幕，就能让您的网站看上去更像原生应用的感觉。

```html
<meta name="viewport" content="width=device-width,                                                           initial-scale=1.0,                                       
maximum-scale=1.0,                                       
user-scalable=no">
```

---

### 排版与链接

Bootstrap 排版、链接样式设置了基本的全局样式。分别是：

+ 为 body 元素设置 background-color: #fff;
+ 使用 @font-family-base、@font-size-base 和 @line-height-base 变量作为排版的基本参数；
+ 为所有链接设置了基本颜色 @link-color ，并且当链接处于 :hover 状态时才添加下划线。

这些样式都能在 scaffolding.less 文件中找到对应的源码。

---

### 布局容器

Bootstrap 需要为页面内容和栅格系统包裹一个 `.container` 容器。我们提供了两个作此用处的类。注意，由于 `padding` 等属性的原因，这两种容器类不能互相嵌套。

`.container` 类用于固定宽度并支持响应式布局的容器。

```html
<div class="container">
  ...
</div>
```

`.container-fluid` 类用于 100% 宽度，占据全部视口（viewport）的容器。

```html
<div class="container-fluid">
  ...
</div>
```

---


## 栅格系统

Bootstrap 提供了一套响应式、移动设备优先的流式栅格系统，随着屏幕或视口（viewport）尺寸的增加，系统会自动分为最多12列。它包含了易于使用的`预定义类`，还有强大的`mixin`用于生成更具语义的布局。

### 简介

栅格系统用于通过一系列的行（row）与列（column）的组合来创建页面布局，你的内容就可以放入这些创建好的布局中。下面就介绍一下 Bootstrap 栅格系统的工作原理：

+ 行（row）”必须包含在 `.container` （固定宽度）或 `.container-fluid`   （100%宽度）中，以便为其赋予合适的排列（aligment）和内补（padding）。
+ 通过“行（row）”在水平方向创建一组“列（column）”。
+ 你的内容应当放置于“列（column）”内，并且，只有“列（column）”可以作为行（row）”的直接子元素。
+ 类似 `.row` 和 `.col-xs-4` 这种预定义的类，可以用来快速创建栅格布局。Bootstrap 源码中定义的 mixin 也可以用来创建语义化的布局。
+ 通过为“列（column）”设置 `padding` 属性，从而创建列与列之间的间隔（gutter）。通过为 `.row` 元素设置负值 `margin` 从而抵消掉为 `.container` 元素设置的 `padding`，也就间接为“行（row）”所包含的“列（column）”抵消掉了`padding`。
+ 负值的 margin就是下面的示例为什么是向外突出的原因。在栅格列中的内容排成一行。
+ 栅格系统中的列是通过指定1到12的值来表示其跨越的范围。例如，三个等宽的列可以使用三个 `.col-xs-4` 来创建。
+ 如果一“行（row）”中包含了的“列（column）”大于 12，多余的“列（column）”所在的元素将被作为一个整体另起一行排列。
+ 栅格类适用于与屏幕宽度大于或等于分界点大小的设备 ， 并且针对小屏幕设备覆盖栅格类。 因此，在元素上应用任何 `.col-md-*` 栅格类适用于与屏幕宽度大于或等于分界点大小的设备 ， 并且针对小屏幕设备覆盖栅格类。 因此，在元素上应用任何` .col-lg-*` 不存在， 也影响大屏幕设备。

---

### 媒体查询

在栅格系统中，我们在 Less 文件中使用以下媒体查询（media query）来创建关键的分界点阈值。

```
/* 超小屏幕（手机，小于 768px） */
/* 没有任何媒体查询相关的代码，因为这在 Bootstrap 中是默认的（还记得 Bootstrap 是移动设备优先的吗？） */

/* 小屏幕（平板，大于等于 768px） */
@media (min-width: @screen-sm-min) { ... }

/* 中等屏幕（桌面显示器，大于等于 992px） */
@media (min-width: @screen-md-min) { ... }

/* 大屏幕（大桌面显示器，大于等于 1200px） */
@media (min-width: @screen-lg-min) { ... }
```

我们偶尔也会在媒体查询代码中包含 max-width 从而将 CSS 的影响限制在更小范围的屏幕大小之内。

```
@media (max-width: @screen-xs-max) { ... }
@media (min-width: @screen-sm-min) and (max-width: @screen-sm-max) { ... }
@media (min-width: @screen-md-min) and (max-width: @screen-md-max) { ... }
@media (min-width: @screen-lg-min) { ... }
```

---

### 栅格参数

通过下表可以详细查看 Bootstrap 的栅格系统是如何在多种屏幕设备上工作的。

|                           | 超小屏幕(<768px) | 小屏幕(≥768px)  | 中等屏幕(≥992px)  | 大屏幕(≥1200px)  |
| ------------------------- |:---------------:| --------------:| ----------------:| ---------------:|
|       **栅格系统行为**    | 总是水平排列    | 开始是堆叠在一起的，当大于这些阈值时将变为水平排列C |
| `.container` **最大宽度** | None （自动）   |  750px         |   970px          |    1170px       |
|        **类前缀**         | .col-xs-        |  .col-sm-      |   .col-md-       |    .col-lg-     |
|    **列（column）数**     |                            12                                         |
|   **最大列（column）宽**  |      自动       |  ~62px         |   ~81px          |    ~97px        |
|    **槽（gutter）宽**     |                     30px （每列左右均有 15px）                        |
|       **可嵌套**          |                                   是                                  |
|     **偏移（Offsets）**   |                                   是                                  |
|       **列排序**          |                                   是                                  |

---

### 实例：从堆叠到水平排列

使用单一的一组 `.col-md-*` 栅格类，就可以创建一个基本的栅格系统，在手机和平板设备上一开始是堆叠在一起的（超小屏幕到小屏幕这一范围），在桌面（中等）屏幕设备上变为水平排列。所有“列（column）必须放在 ” `.row` 内。

---

### 实例：流式布局容器

将最外面的布局元素 `.container` 修改为 `.container-fluid`，就可以将固定宽度的栅格布局转换为 100% 宽度的布局。

```html
<div class="container-fluid">
  <div class="row">
    ...
  </div>
</div>
```
---

### 实例：移动设备和桌面屏幕

使用针对超小屏幕和中等屏幕设备所定义的类，即 `.col-xs-*` 和 `.col-md-*`。

---

### 实例：手机、平板、桌面

在上面案例的基础上，通过使用针对平板设备的 .col-sm-* 类，来创建更加动态和强大的布局.

---

### 实例：多余的列（column）将另起一行排列

如果在一个 `.row` 内包含的列（column）大于12个，包含多余列（column）的元素将作为一个整体单元被另起一行排列。

---

### 响应式列重置

即便有上面给出的四组栅格class，你也不免会碰到一些问题，例如，在某些阈值时，某些列可能会出现比别的列高的情况。为了克服这一问题，建议联合使用 `.clearfix` 和 **响应式工具类**。

--- 

### 列偏移

使用 `.col-md-offset-*` 类可以将列向右侧偏移。这些类实际是通过使用 * 选择器为当前元素增加了左侧的边距（margin）。例如，`.col-md-offset-4` 类将 `.col-md-4 `元素向右侧偏移了4个列（column）的宽度。

---

### 嵌套列

为了使用内置的栅格系统将内容再次嵌套，可以通过添加一个新的 `.row `元素和一系列 `.col-sm-*` 元素到已经存在的 `.col-sm-*` 元素内。被嵌套的行（row）所包含的列（column）的个数不能超过12（其实，没有要求你必须占满12列）。

---

### 列排序

通过使用 `.col-md-push-*`和 `.col-md-pull-*` 类就可以很容易的改变列（column）的顺序。

---

### Less mixin 和变量

-------


## 排版

---

### 标题

HTML 中的所有标题标签，<h1> 到 <h6> 均可使用。另外，还提供了 .h1 到 .h6 类，为的是给内联（inline）属性的文本赋予标题的样式。

在标题内还可以包含 `<small>` 标签或赋予 `.small` 类的元素，可以用来标记副标题。

---

### 页面主体

Bootstrap 将全局 `font-size` 设置为 14px，`line-height` 设置为 1.428。这些属性直接赋予 `<body>` 元素和所有段落元素。另外，`<p> `（段落）元素还被设置了等于 1/2 行高（即 10px）的底部外边距（margin）。

#### 中心内容

通过添加 .lead 类可以让段落突出显示。

```
<p class="lead">...</p>
```

#### 使用 Less 工具构建

**variables.less** 文件中定义的两个 Less 变量决定了排版尺寸：`@font-size-base` 和 `@line-height-base`。第一个变量定义了全局 font-size 基准，第二个变量是 line-height 基准。我们使用这些变量和一些简单的公式计算出其它所有页面元素的 margin、 padding 和 line-height。自定义这些变量即可改变 Bootstrap 的默认样式。

---

### 内联文本元素

For highlighting a run of text due to its relevance in another context, use the `<mark>` tag.

#### 被删除的文本

对于被删除的文本使用 `<del>` 标签。

```html
效果:<del>hello world</del>
```

#### 无用文本

对于没用的文本使用 `<s>` 标签。

```html
效果:<s>hello world</s>
```

#### 插入文本

额外插入的文本使用 `<ins>` 标签。

```html
效果:<ins>hello world</ins>
```

#### 带下划线的文本

为文本添加下划线，使用 `<u>` 标签。

```html
效果:<u>hello world</u>
```

利用 HTML 自带的表示强调意味的标签来为文本增添少量样式。

#### 小号文本

对于不需要强调的inline或block类型的文本，使用 `<small>` 标签包裹，其内的文本将被设置为父容器字体大小的 85%。标题元素中嵌套的 `<small>` 元素被设置不同的 font-size 。

还可以为行内元素赋予 .small 类以代替任何 `<small>` 元素。

#### 着重

通过增加 font-weight 值强调一段文本(`<strong>`)。

#### 斜体

用斜体强调一段文本(`<em>`)。

在 HTML5 中可以放心使用 `<b>` 和 `<i>` 标签。`<b>` 用于高亮单词或短语，不带有任何着重的意味；而 `<i>` 标签主要用于发言、技术词汇等。

---

###　对齐

通过文本对齐类，可以简单方便的将文字重新对齐。

```html
<p class="text-left">Left aligned text.</p>
<p class="text-center">Center aligned text.</p>
<p class="text-right">Right aligned text.</p>
<p class="text-justify">Justified text.</p>
<p class="text-nowrap">No wrap text.</p>
```

---

### 改变大小写

通过这几个类可以改变文本的大小写。

```html
<p class="text-lowercase">Lowercased text.</p>
<p class="text-uppercase">Uppercased text.</p>
<p class="text-capitalize">Capitalized text.</p>
```

---

### 缩略语

当鼠标悬停在缩写和缩写词上时就会显示完整内容，Bootstrap 实现了对 HTML 的 `<abbr>` 元素的增强样式。缩略语元素带有 title 属性，外观表现为带有较浅的虚线框，鼠标移至上面时会变成带有“问号”的指针。如想看完整的内容可把鼠标悬停在缩略语上（对使用辅助技术的用户也可见）, 但需要包含 title 属性。

#### 基本缩略语

```
<abbr title="attribute">attr</abbr>
```

#### 首字母缩略语

为缩略语添加 `.initialism` 类，可以让 font-size 变得稍微小些。

---

### 地址

让联系信息以最接近日常使用的格式呈现。在每行结尾添加 <br> 可以保留需要的样式。

```html
<address>
  <strong>Twitter, Inc.</strong><br>
  1355 Market Street, Suite 900<br>
  San Francisco, CA 94103<br>
  <abbr title="Phone">P:</abbr> (123) 456-7890
</address>

<address>
  <strong>Full Name</strong><br>
  <a href="mailto:#">first.last@example.com</a>
</address>
```

---

### 引用

在你的文档中引用其他来源的内容。

#### 默认样式的引用

将任何 HTML 元素包裹在 `<blockquote>` 中即可表现为引用样式。对于直接引用，我们建议用 <p> 标签。

#### 多种引用样式

对于标准样式的 `<blockquote>`，可以通过几个简单的变体就能改变风格和内容。

##### 命名来源

添加 `<footer>` 用于标明引用来源。来源的名称可以包裹进 <cite>标签中。

```html
<blockquote>
  <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer posuere erat a ante.</p>
  <footer>Someone famous in <cite title="Source Title">Source Title</cite></footer>
</blockquote>
```

另一种展示风格

通过赋予 `.blockquote-reverse `类可以让引用呈现内容右对齐的效果。

```html
<blockquote class="blockquote-reverse">
  ...
</blockquote>
```

---

### 列表

#### 无序列表

排列顺序无关紧要的一列元素。

```
<ul>
  <li>...</li>
</ul>
```

#### 有序列表

顺序至关重要的一组元素。

```
<ol>
  <li>...</li>
</ol>
```

#### 无样式列表

移除了默认的 `list-style` 样式和左侧外边距的一组元素（只针对直接子元素）。这是针对直接子元素的，也就是说，你需要对所有嵌套的列表都添加这个类才能具有同样的样式。

```
<ul class="list-unstyled">
  <li>...</li>
</ul>
```

#### 内联列表

通过设置 `display: inline-block`; 并添加少量的内补（padding），将所有元素放置于同一行。

```
<ul class="list-inline">
  <li>...</li>
</ul>
```

#### 描述

带有描述的短语列表。

```
<dl>
  <dt>...</dt>
  <dd>...</dd>
</dl>
```

##### 水平排列的描述

`.dl-horizontal` 可以让 `<dl>` 内的短语及其描述排在一行。开始是像 `<dl> `的默认样式堆叠在一起，随着导航条逐渐展开而排列在一行。

```
<dl class="dl-horizontal">
  <dt>...</dt>
  <dd>...</dd>
</dl>
```
----

>自动截断
>通过 text-overflow 
>属性，水平排列的描述列表将会截断左侧太长的短语。在较窄的视口（viewport）内，列表将变为默认堆叠排列的布局方式。

---

`---待更新---`

[个人微博](http://www.weibo.com/1x24)

---