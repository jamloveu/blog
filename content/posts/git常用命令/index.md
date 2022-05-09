---
title: "git常用命令"
subtitle: ""
date: 2018-04-15T01:31:02+08:00
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

```
git log // 查询要回滚的 commit_id
git reset --hard commit_id // HEAD 就会指向此次的提交记录
git push origin HEAD --force // 强制推送到远端
```