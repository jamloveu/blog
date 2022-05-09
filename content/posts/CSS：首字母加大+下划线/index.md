---
title: "首字母加大+下划线"
subtitle: ""
date: 2017-04-15T01:49:53+08:00
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
```

<!doctype html>
<html>
	<head>
		<style type="text/css">
			.text{
				font-family:Times New Roman;
				font-size:24px;
				float:left;
				clear:left;
				width:auto;
			}
			.text:first-letter{
				font-size:48px;
			}
			.text:after {
				content:'';
				display:block;
				margin-top:-5px;
				border-bottom:2px solid grey;
			}
		</style>
		<script src="js/jquery-1.8.2.min.js">
			$(document).ready(function(){
				$(.text).each(function(){
					$(this:after).css("width",$(this).css("width"));
				});
			});
		</script>
	</head>
	<body>
		<div class="text">About</div>
		<div class="text">Technology</div>
	</body>
</html>
```

![image](91327C1B807B4598BA8275E4BC969B5A)