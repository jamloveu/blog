---
title: "redace方法"
subtitle: ""
date: 2019-04-15T01:34:09+08:00
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

###### 问题：
```
[
  {id:'001', num:10},
  {id:'002', num:8}
]
把这个数组对象变成 : { '001': 10, '002': 8}
```
###### 方法一
```
let list = [
      {id:'001', num:10},
      {id:'002', num:8}
]
let obj = {}
list.forEach(item=>{
    obj[item.id] = item.num
})
```

###### 方法二
```
[
  {id:'001', num:10},
  {id:'002', num:8}
].reduce( (obj, item)=> {
  obj[item.id] = item.num
  return obj
} ,{})
```
```
[
  {id:'001', num:10},
  {id:'002', num:8}
].reduce( (obj, item)=>({...obj, [item.id]: item.num}) ,{})

不可变数据写法
```