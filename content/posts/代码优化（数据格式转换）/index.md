---
title: "代码优化（数据格式转换）"
subtitle: ""
date: 2018-04-15T01:41:32+08:00
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

在接口请求等情况，需要取出有用的字段
```
const data =
{
    activityId: "332d388d-deb3-49ce-87d6-d564bdf37ad6"
    courseId: "f3153d06-4f65-4833-a52b-1bfbc806141d"
    cover: "/UploadFiles/20201112140303911_1_134.jpg"
    price: 0.01
    quantityBought: 0
    skillPrice: 0.01
    stock: 1
    tag: "秒杀"
    title: "前端系统教程"
}
```
转换为下面的数据格式
```
const result = {
    activityId: "332d388d-deb3-49ce-87d6-d564bdf37ad6"
    courseId: "f3153d06-4f65-4833-a52b-1bfbc806141d"
    cover: "https://renda.saas.senparc.com/UploadFiles/20201112140303911_1_134.jpg"
    price: 0.01
    title: "前端系统教程"
    totalPrice: 0.01
}
```
#### 方案一
```
const list = {
    activityId: data.activityId, //活动id
    courseId: data.courseId, //课程id
    cover: IMG_PATH + data.cover, //封面
    title: data.title, //标题
    price: data.skillPrice, //课程价格
    totalPrice: data.skillPrice //合计价格
     }
```
#### 方案二
```
let list2 = {};
    Object.keys(data).forEach((i) => {
        list2.activityId = data[i].activityId;
        list2.courseId = data[i].courseId;
        list2.cover = IMG_PATH + data[i].cover;
        list2.title = data[i].title;
        list2.price = data[i].skillPrice;
        list2.totalPrice = data[i].skillPrice;
    })
```
#### 方案三
```
const list3 = {
    ...data,
    cover: IMG_PATH + data.cover, //封面
    price: data.skillPrice, //课程价格
    totalPrice: data.skillPrice //合计价格
}
```
### 方案四
```
const { activityId, courseId, cover, title, skillPrice: price } = data
const list4 = {
        activityId,
        courseId,
        cover: IMG_PATH + cover,
        title,
        price,
        totalPrice: price
}
```