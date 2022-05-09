---
title: "CSS:单行文本溢出和多行文本溢出"
subtitle: ""
date: 2019-04-15T01:39:49+08:00
draft: false
author: ""
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
#### 单行文本溢出省略号
核心代码就三行:
```
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
```

**demo:**
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
  <style>
  div{
  border: 1px solid red;
  max-width:200px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
  </style>
</head>
<body>
<div>11111111111111111118877777777777777777</div>
</body>
</html>
```

#### 多行文本溢出省略号
核心代码四行:
```
display: -webkit-box;
-webkit-box-orient: vertical;
-webkit-line-clamp: 2;
overflow: hidden;
```
`-webkit-line-clamp: 2;` 可以设置行数

**demo:**
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
  <style>
  div{
  border: 1px solid red;
  max-width:100px;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 3;
  overflow: hidden;

}
  </style>
</head>
<body>
<div>111111111111111111113333333333
  1111111111111111111111
  111118855555555555
  77777777777
  777777</div>
</body>
</html>
```