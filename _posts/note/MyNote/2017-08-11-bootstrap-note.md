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

#### HTML5 文档类型

Bootstrap 使用了一些 HTML5 元素和 CSS 属性。Bootstrap 项目的开头包含下面的代码段：

```html
<!DOCTYPE html>
<html>
....
</html>
```

如果在 Bootstrap 创建的网页开头不使用 HTML5 的文档类型（Doctype），您可能会面临一些浏览器显示不一致的问题，甚至可能面临一些特定情境下的不一致，以致于您的代码不能通过 W3C 标准的验证。

---

#### 移动设备优先

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

#### 排版与链接

Bootstrap 排版、链接样式设置了基本的全局样式。分别是：

+为 body 元素设置 background-color: #fff;
+使用 @font-family-base、@font-size-base 和 @line-height-base 变量作为排版的基本参数；
+为所有链接设置了基本颜色 @link-color ，并且当链接处于 :hover 状态时才添加下划线。

这些样式都能在 scaffolding.less 文件中找到对应的源码。

---

#### 布局容器

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

`---待更新---`

---