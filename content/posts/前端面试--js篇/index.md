---
title: "前端面试--js篇"
subtitle: ""
date: 2022-04-15T22:12:48+08:00
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
## 1、JS数据类型有哪些？
### 基本概念
一共八种：数字、字符串、布尔、null、undefined、对象、symbol、bigint
```
number、string、Boolean、null、undefined、object、symbol、bigint
```

### 推展
- 表示一个对象为空用null，表示一个非对象为空，用undefiend
- symbol、bigint的新加的。
- 用bigint？js的number默认是一个双精度浮点数，位数是有限的。使用方法是数字后面加一个n，比如：12345678912345677n

```
输入-> 12345678912345677
输出<- 12345678912345676

输入-> 12345678912345677n
输出<- 12345678912345677n
```

- bigint只支持整数，不支持小数
- symbol日常开发几乎没有用，一般做库需要用到

- 提了就0分的答案：数组、函数、日期。这些是类，不是类型。


## 2、原型链是什么？
