---
title: "什么是BFC"
subtitle: ""
date: 2019-04-15T01:42:16+08:00
draft: false
author: "jam"
authorLink: ""
description: ""
keywords: ""
license: ""
comment: false
weight: 0

tags:
- draft
categories:
- draft

hiddenFromHomePage: false
hiddenFromSearch: false

summary: ""
resources:
- name: featured-image
  src: featured-image.jpg
- name: featured-image-preview
  src: featured-image-preview.jpg

toc:
  enable: true
math:
  enable: false
lightgallery: false
seo:
  images: []

# See details front matter: /theme-documentation-content/#front-matter
---

<!--more-->
昨天晚上看了BFC，写笔记记录一下。

## CSS规范中对 BFC 的描述
9.4.1 块格式化上下文（Block Formatting Context，BFC）

浮动，绝对定位元素，非块盒的块容器（例如，inline-blocks，table-cells和table-captions）和'overflow'不为'visible'的块盒会为它们的内容建立一个新的块格式化上下文

在一个块格式化上下文中，盒在竖直方向一个接一个地放置，从包含块的顶部开始。两个兄弟盒之间的竖直距离由'margin'属性决定。同一个块格式化上下文中的相邻块级盒之间的竖直margin会合并

在一个块格式化上下文中，每个盒的left外边（left outer edge）挨着包含块的left边（对于从右向左的格式化，right边挨着）。即使存在浮动（尽管一个盒的行盒可能会因为浮动收缩），这也成立。除非该盒建立了一个新的块格式化上下文（这种情况下，该盒自身可能会因为浮动变窄）

## MDN 对 BFC 的描述
一个块格式化上下文（block formatting context） 是Web页面的可视化CSS渲染出的一部分。它是块级盒布局出现的区域，也是浮动层元素进行交互的区域。

一个块格式化上下文由以下之一创建：

- 根元素或其它包含它的元素
- 浮动元素 (元素的 float 不是 none)
- 绝对定位元素 (元素具有 position 为 absolute 或 fixed)
- 内联块 (元素具有 display: inline-block)
- 表格单元格 (元素具有 display: table-cell，HTML表格单元格默认属性)
- 表格标题 (元素具有 display: table-caption, HTML表格标题默认属性)
- 具有overflow 且值不是 visible 的块元素，
- display: flow-root
- column-span: all 应当总是会创建一个新的格式化上下文，即便具有 column-span: all 的元素并不被包裹在一个多列容器中。


一个块格式化上下文包括创建它的元素内部所有内容，除了被包含于创建新的块级格式化上下文的后代元素内的元素。

块格式化上下文对于定位 (参见 float) 与清除浮动 (参见 clear) 很重要。定位和清除浮动的样式规则只适用于处于同一块格式化上下文内的元素。浮动不会影响其它块格式化上下文中元素的布局，并且清除浮动只能清除同一块格式化上下文中在它前面的元素的浮动。

## 张鑫旭对 BFC 的描述

`http://www.zhangxinxu.com/wordpress/2015/02/css-deep-understand-flow-bfc-column-two-auto-layout/`

BFC全称”Block Formatting Context”, 中文为“块级格式化上下文”。啪啦啪啦特性什么的，一言难尽，大家可以自行去查找，我这里不详述，免得乱了主次，总之，记住这么一句话：BFC元素特性表现原则就是，内部子元素再怎么翻江倒海，翻云覆雨都不会影响外部的元素。所以，避免margin穿透啊，清除浮动什么的也好理解了

emmmmm，全部没看懂！

## 妈的，BFC 到底是什么？

先思考一个问题：

请问：什么是色情？

联邦最高法院大法官斯图尔特更有一句名言：

我不知道什么是色情，不过，我看了之后，就能知道

`I know it when I see it`

类似地：

1. 我不知道什么是 BFC
1. 但是你写出样式，我就知道这是不是 BFC

BFC 就是这样的东西（堆叠上下文也是）

1. 它没有定义
2. 它只有特性/功能

## 功能1：爸爸管儿子
用 BFC 包住浮动元素。(这 TM 不是清除浮动，.clearfix 才是清除浮动）

```
<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
  <style>
    .baba{
      border: 10px solid red;
      min-height: 10px;
      /*触发BFC的条件*/
      /* display: flow-root;  */
      /*display: inline-block;*/
      /*float: left;*/
      /*position: absolute;*/
      overflow: auto;
      
    }
    .erzi{
      background: green;
      float:left;
      width: 300px;
      height: 100px;
    }
  </style>
</head>

<body>
  <div class="baba">
    <div class="erzi">
    </div>
  </div>
</body>

</html>
```

`演示地址：http://js.jirengu.com/rozaxufetu/1/edit?html,css,output`
## 功能2：兄弟之间划清界限
用 float + div 做左右自适应布局

```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
  <style>
    .gege{
      width: 100px;
      min-height: 600px;
      border: 3px solid red;
      float: left;
      margin-right: 20px;
    }
    .didi{
      min-height: 600px;
      border: 5px solid green;
      display: flow-root;
    }
  </style>
</head>
<body>
  <div class="gege">gege</div>
  <div class="didi">1234</div>
</body>
</html>
```

`演示地址：http://js.jirengu.com/felikenuve/1/edit?html,css,output`