---
title: "CSS3背景"
subtitle: ""
date: 2017-04-15T01:36:10+08:00
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
#### 1.基本属性
- `background-color`
- `background-image`
- `background-repeat`
- `background-attachment`
- `background-position`

#### 2.背景原点属性
- `background-origin`

#### 3.背景裁剪属性
- `background-clip`

#### 4. 背景尺寸
- `background-size`

#### 5.内联元素背景图像平铺循环方式
- `background-break`

#### 6.多背景属性
```
background:[background-image] | [background-position][/background-size] | [background-repeat] | [background-attachment] | [background-clip] | [background-origin],*

```
除了background-color以外，其他的属性都可以设置多个属性值，不过前提的元素有多个背景图像存在。多个属性值之间必须用逗号分开。