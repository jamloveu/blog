---
title: "常用的javascript代码片段"
subtitle: ""
date: 2019-04-15T01:23:01+08:00
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

# 1.复制文本
```
function copyToClip(content, message){
  let aux = document.createElement("input");
  aux.setAttribute("value", content);
  document.body.appendChild(aux);
  aux.select();
  document.execCommand("copy");
  document.body.removeChild(aux);
  if (!message) {
   alert('复制成功')
  } else {
    alert(message)
  }
}
```

# 2.富文本正则替换图片的src
```
/**
 * 富文本内的图片兼容处理
 * content: 富文本内容
*/
const richTextImage2FullPath = (content)=>{
  let c = content.replace(/(<img[\s\S]+?)src=(['"][^'"]+)['"]/ig, function (match, capture,$1) {
      // console.log('$1', $1);
      // console.log('match', match);
      // console.log('capture', capture);
      let c = $1.replace('"/','/')
      let b =c.replace("'/",'/')
      let d = getFullPathImage(b)
      return `${capture} src='${d}'`
  });
  return c
}
```
