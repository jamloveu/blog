---
title: "在github上建新项目"
subtitle: ""
date: 2017-04-15T01:49:17+08:00
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
一、在本地建并上传到github上。
步骤：
1. `mkdir git-demo-1` 创建目录
2.  `cd git-demo-1`  进入目录
3.  `git init`  初始化git
4.  `ls -la`  看一下（可选）
5.  添加文件
-  `touch index.js`  创建文件index.js
-  `mkdir js`   创建文件夹js
-  `mv index.js js/`  移动index.js到js文件夹
6. `git status -sb` 查看一下（可选）
7. `git add .`  将所有文件加到暂缓区。也可以`git add index.js` 将指定文件index.js加到暂缓区
8. `git status -sb`  再看一下（可选）
9. `git commit . -m "添加了几个文件"`   将所有文件正式提交到本地仓库，并加注释。也可以`git commit index.js -m '添加index.js'` 将指定文件加到本地仓库。
10. `git status -sb`  再看一下状态（可选）
11. `git log`  再查看一下历史变动（可选）
12. 在github上新建一个空仓库，什么都不动就可以了。
13. `git remote add origin git@github.com:Jamamm/git-demo-1.git`
14. `git push -u origin master`  选择SSH,复制第二块命令就行了。因为前面已经执行了第一块的部分命令。

简化：
1. `git init` 
2. `git git add .`
3. `git commit . -m "添加了几个文件"`
4. `git remote add origin git@github.com:Jamamm/git-demo-1.git`
5. `git push -u origin master`


二、在github上新建仓库并下载下来。
1. 填写项目名称
2. 选中第三项`Initialize this repository with a README`，并且选择
     `Add .gitignore: Node`
     `Add a license:MIT License`
3. 然后`git clone 项目地址`就可以了