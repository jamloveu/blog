---
title: "CSS：Flex布局"
subtitle: ""
date: 2017-04-15T01:51:03+08:00
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
阮一峰的flex教程：http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html

小游戏：http://flexboxfroggy.com/#zh-cn       http://www.flexboxdefense.com/

#### 在Flex之前我们用什么布局？
```

normal flow（正常流，也叫文档流）

float + clear

position relative + absolute

display inline-block

负 margin
```


#### CSS3 的Flex布局来了
```
块级布局侧重垂直方向，行内布局侧重水平方向，FLex布局是与方向无关的。

FLex布局可以实现空间自动分配、自动对齐（flexible：弹性、灵活）

flex适用于简单的线性布局，更复杂的布局要交给 grid 布局（还没发布）
```






如果把一个`<div class="parent">`里面的`<div classs="son">`垂直水平居中？

`<div class="parent">`上面加
```
{
display: flex;
justify-content: center;
align-iteams: center;
}
```


#### flex containter 的属性:
```
flex-direction   属性决定主轴的方向（即项目的排列方向）。
flex-wrap        换行。默认情况下，项目都排在一条线（又称"轴线"）上。flex-wrap属性定义，如果一条轴线排不下，如何换行。
flex-flow        上面两个的简写
justify-content  主轴方向对齐方式
align-items      交叉轴上对齐方式
align-content    多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。
```





##### 一
```
flex-direction（方向）的值
    row				从左往右
    row-reverse		从右向左（反向排列）
    column			从上往下
    column-reverse	从下往上
    inherit
    initial
    unset
```
##### 二
```
flex-wrap（换行）的值
    wrap			换行
    no-wrap			不换行

```

##### 三

```
flex-flow是flex-direction和flex-wrap的简写
flex-flow: row nowrap;
```
##### 四

```
justify-content 的五个值
flex-start  		往起点靠
flex-end   		往终点靠
center			居中
space-between	空间放在中间
space-around		空间放在周围
```


##### 五
```
align-items的值
flex-start			往起点靠
stretch			伸展
center			居中
```


##### 六
```
align-content 多行/列内容对齐方式（用得较少）
```

```
flex iteam 的属性
flex-grow		增长比例（空间过多时）
flex-shrink	收缩比例（空间不够时）
flex-basis		默认大小（一般不用）
flex			上面三个的缩写
order		顺序（代替双飞翼）
align-self		自身的对齐方式
```

