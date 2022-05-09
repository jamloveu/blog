---
title: "CSS基础入门"
subtitle: ""
date: 2017-04-15T01:40:48+08:00
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
## 层叠样式表（英语：Cascading Style Sheets，简写CSS）

## 发展历史：
1. 两个人合作发明了 CSS
1994年哈肯·维姆·莱提出了CSS的最初建议。伯特·波斯（Bert Bos）当时正在设计一个叫做“Argo”的浏览器，他们决定一起合作设计CSS。
W3C 开始接管 CSS

2. 1997年初，W3C内组织了专门管CSS的工作组，其负责人是克里斯·里雷。
CSS 2.1
3. 1998年5月W3C发表了CSS2
CSS2.1修改了CSS2中的一些错误，删除了其中基本不被支持的内容和增加了一些已有的浏览器的扩展内容。
4. CSS 3
从 2011 年开始 CSS 被分为多个模块单独升级，统称为 CSS 3。这些模块有：
CSS 选择器 level 3
CSS 媒体查询 level 3
CSS Color level 3
更多请 搜索 CSS spec
5. CSS 4?
不好意思，没有 CSS 4，只有各个模块的 level 4

CSS 学习资源
1. Google: 关键词 MDN
2. CSS Tricks https://css-tricks.com/
3. Google: 阮一峰 css https://www.google.com/search?q=%E9%98%AE%E4%B8%80%E5%B3%B0+css
4. 张鑫旭的 240 多篇 CSS 博客 https://www.zhangxinxu.com/wordpress/category/css/page/25/
5. Codrops 炫酷 CSS 效果 https://tympanus.net/codrops/category/playground/
6. CSS揭秘 http://www.ituring.com.cn/book/1695
7. CSS 2.1 中文 spec
8. Magic of CSS 免费在线书 https://adamschwartz.co/magic-of-css/


# css布局 
## 浮动
通过在元素身上加：`float: left/right;`，达到元素横向排列的目的。

## 清除浮动
浮动元素不再占有文档流的位置，因此会对后面元素的排版造成影响。
清除浮动的几种常用方式：
1. 额外标签法
2. 父级添加overflow属性方法
3. 使用after伪元素清除
4. 使用before和after双伪元素清除

一、 额外标签法：
```
是W3C推荐的做法是通过在浮动元素末尾添加一个空的标签例如 <div style=”clear:both”></div>，或则其他标签br等亦可。
```
结构较差，不推荐

二、 父级添加overflow属性方法
```
可以给父级添加： overflow 为 hidden|auto|scroll  都可以实现。
```

三、 使用after伪元素清除
浮动元素的父元素身上加 `clearfix`
```
 .clearfix:after {  content: ""; display: block; height: 0; clear: both; visibility: hidden;  }   

 .clearfix {*zoom: 1;}   /* IE6、7 专有 */
```
或者这样写
```
clearfix:after{
content: '';
dispaly: block;
clear: both;
}
```

四、 使用before和after双伪元素清除
和三一样，在浮动元素父元素身上加`clearfix`
```
.clearfix:before,.clearfix:after { 
  content:"";
  display:table;  /* 这句话可以触发BFC BFC可以清除浮动 */
}
.clearfix:after {
 clear:both;
}
.clearfix {
  *zoom:1;
}
```

### display和visibility
...

---



### css的选择器
1. 标签
2. 类名
3. 多类名
4. id选择器
5. 通配符选择器
6. 伪类和伪元素选择器
7. 其他

### 字体样式
1. **font-size**`单位：em（相对尺寸）、px（像素）、in（英寸）、cm（厘米）、mm（毫米）、pt（点）`
2. **font-family**
3. **font-weight** `字体粗细，normal(400)、bold(700)、bolder、lighter、100~900（100的整数倍）` 
4. **综合：font: font-style  font-weight  font-size/line-height  font-family;**

### 外观
1. **color**
2. **line-height 行间距**
3. **text-align**  `left/right/center`
4. **text-indent 首行缩进**
5. **text-decoration文本装饰**  `none/underline下划线/overline线在上/line-through线在中间`
6. 

### 隐藏样式
 1. display: none           
 2. display: block ;  显示的意思 
 3. visibility: hidden;      
 4. visibility: visible  显示的意思
 5. display  隐藏不占位置
 6. visibility:hidden 隐藏占有位置   停职留心
 7. overflow:hidden;   隐藏超出的部分。