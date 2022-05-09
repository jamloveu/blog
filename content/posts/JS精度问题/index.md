---
title: "JS精度问题"
subtitle: ""
date: 2018-04-15T01:31:54+08:00
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

//解决js计算精度问题
// 为了保证小数相加减出现精度溢出的问题
const calcPlus = (num1, num2) => {
	let baseNum, baseNum1, baseNum2;
	try {
		baseNum1 = num1.toString().split('.')[1].length;
	} catch (e) {
		baseNum1 = 0;
	}
	try {
		baseNum2 = num2.toString().split('.')[1].length;
	} catch (e) {
		baseNum2 = 0;
	}
	baseNum = Math.pow(10, Math.max(baseNum1, baseNum2));
	let precision = baseNum1 >= baseNum2 ? baseNum1 : baseNum2; //精度
	return ((num1 * baseNum + num2 * baseNum) / baseNum).toFixed(precision);
}

// 为了保证小数相加减出现精度溢出的问题
const calcMinus = (num1, num2) => {
	let baseNum, baseNum1, baseNum2;
	try {
		baseNum1 = num1.toString().split('.')[1].length;
	} catch (e) {
		baseNum1 = 0;
	}
	try {
		baseNum2 = num2.toString().split('.')[1].length;
	} catch (e) {
		baseNum2 = 0;
	}
	baseNum = Math.pow(10, Math.max(baseNum1, baseNum2));
	let precision = baseNum1 >= baseNum2 ? baseNum1 : baseNum2;
	return ((num1 * baseNum - num2 * baseNum) / baseNum).toFixed(precision);
}

// 乘法
const calcMultiply = (arg1, arg2) => {
	let m = 0,
		s1 = arg1.toString(),
		s2 = arg2.toString();
	try {
		m += s1.split(".")[1].length
	} catch (e) {}
	try {
		m += s2.split(".")[1].length
	} catch (e) {}
	return Number(s1.replace(".", "")) * Number(s2.replace(".", "")) / Math.pow(10, m)
}

// 除法
const calcDivide = (arg1, arg2) => {
	let t1 = 0,
		t2 = 0,
		r1, r2;
	try {
		t1 = arg1.toString().split(".")[1].length
	} catch (e) {}
	try {
		t2 = arg2.toString().split(".")[1].length
	} catch (e) {}

	r1 = Number(arg1.toString().replace(".", ""))
	r2 = Number(arg2.toString().replace(".", ""))
	return (r1 / r2) * Math.pow(10, t2 - t1);
}

```