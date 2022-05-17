---
title: "Mockjs教程"
subtitle: ""
date: 2022-05-17T22:54:26+08:00
draft: false
author: "Jam"
authorLink: ""
description: ""
keywords: ""
license: ""
comment: false
weight: 0

tags:
- Mock
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

# 什么是mockjs
Mock.js 是一款前端开发中拦截Ajax请求再生成随机数据响应的工具.可以用来模拟服务器响应. 优点是非常简单方便, 无侵入性, 基本覆盖常用的接口数据类型.
- 前后端分离
- 开发无侵入（不需要修改既有代码，就可以拦截 Ajax 请求，返回模拟的响应数据。）
- 数据类型丰富（支持生成随机的文本、数字、布尔值、日期、邮箱、链接、图片、颜色等。）
- 增加单元测试的真实性（通过随机数据，模拟各种场景。）
- 用法简单、符合直觉的接口。
- 方便扩展（支持支持扩展更多数据类型，支持自定义函数和正则。）

# 开始 & 安装

推荐使用npm的方式。
```js
# 安装
npm install mockjs

// 使用 Mock
var Mock = require('mockjs')
var data = Mock.mock({
    // 属性 list 的值是一个数组，其中含有 1 到 10 个元素
    'list|1-10': [{
        // 属性 id 是一个自增数，起始值为 1，每次增 1
        'id|+1': 1
    }]
})
// 输出结果
console.log(JSON.stringify(data, null, 4))
```

# mock语法

## 生成字符串

- 生成指定次数字符串

```js
import Mock from 'mockjs'
const data = Mock.mock({
"string|4":"哈哈"
})
```

- 生成指定范围长度字符串

```js
const data = Mock.mock({
"string|1-8":"哈哈"
})
```

## 生成文本

- 生成一个随机字符串

```js
const data = Mock.mock({
	"string":"@cword"
}) 
```

- 生成指定长度和范围

```js
const data = Mock.mock({
    string:"@cword(1)"
    str :"@cword(10,15)"
})
```

## 生成标题和句子

- 生成标题和句子

```js
const data = Mock.mock({
    title:"@ctitle(8)"
    sentence:"@csentence"
})
```

- 生成指定长度的标题和句子

```js
const data = Mock.mock({
    title:"@ctitle(8)"
    sentence:"@csentence(50)"
})
```

- 生成指定范围的

```js
const data = Mock.mock({
    title:"@ctitle(5,8)"
    sentence:"@csentence(50,100)"
})
```

## 生成段落

- 随机生成段落

```js
const data = Mock.mock({
  content:"@cparagraph()"
})
```

## 生成数字

- 生成指定数字

```js
const data = Mock.mock({
	"number|80":1
})
```

- 生成范围数字

```js
const data = Mock.mock({
	"number|1-99":1
})
```

## 生成自增id

- 随机生成标识

```js
const data = Mock.mock({
	id:"@increment"
})
```

## 生成姓名-地址-身份证

- 随机生成姓名-地址-身份证

```js
const data = Mock.mock({
	name:"@cname()"
	idCard:"@id()"
	address:"@city(true)"
})
```

## 随机生成图片

- 生成图片：@image（“300*200”，‘#ff0000','#fff','gif','坤坤'）
- 参数1：图片大小

```
[
	'300*250','250*250','240*400','336*280'
	'180*150','720*300','468*60','234*60'
	'388*31','250*250','240*400','120*40'
	'125*125','250*250','240*400','336*280'
]
```

- 参数2：图片背景色
- 参数3：图片前景色
- 参数4：图片格式
- 参数5：图片文字

## 生成时间

- @Date
- 生成指定格式时间：@date(yyyy-MM-dd hh:mm:ss)

指定数组返回的参数

- 指定长度：‘date|5’
- 指定范围:'data|5-10'

```js
const data = Mock.mock({
'list|50-99':[
        {
            name:'@cname'
            address:'@city(true)'
            id:'@increment()'
        }	
    ]
})
```

# mock拦截请求

## 定义get请求

```js
Mock.mock('api/get/news','get',()=>{
    return{
        status:200,
        message:"获取数据成功"
    }
})
```

## 定义post请求

```js
Mock.mock('api/post/news','post',()=>{
    return{
        status:200,
        message:"获取数据成功"
    }
})
```

# 实现新闻管理案例

## 获取数据

接口地址：：/api/get/news

接口参数：

```js
// pageindex：页码
// pagesize:每页的条数
```

请求类型：get

返回的数据：

```json
{
    status:200,
        message:"获取新闻列表成功",
        list:[
        {
            "id":1,
            "title":"解忧杂货店",
            "content":"《解忧杂货店》是日本作家东野圭吾写作的长篇小说。2011年《小说野性时代》连载，于2012年3月由角川书店发行单行本",
            "img_url":"http://t15.baidu.com/it/u=2090705107,20534764&fm=224&app=112&f=JPEG?w=500&h=500&s=61D0718656561FFFE504A51703000067",
            "add_time":"1984-04-03 11:43:37"}
        ],
        total:50
    }
}
```

## 添加新闻

接口地址：：/api/add/news

接口参数：

```
title：'标题'
content：内容
```

请求类型：post

返回的数据：

```json
{
    status:200,
        message:"获取新闻列表成功",
        list:[
        {
            "id":1,
            "title":"解忧杂货店",
            "content":"《解忧杂货店》是日本作家东野圭吾写作的长篇小说。2011年《小说野性时代》连载，于2012年3月由角川书店发行单行本",
            "img_url":"http://t15.baidu.com/it/u=2090705107,20534764&fm=224&app=112&f=JPEG?w=500&h=500&s=61D0718656561FFFE504A51703000067",
            "add_time":"1984-04-03 11:43:37"}
        ],
        total:50
    }
}
```



## 删除新闻

接口地址：：/api/delete/news

接口参数：

```
id；新闻id
```

请求类型：post

返回的数据：

```
{
    status:200,
        message:"获取新闻列表成功",
        list:[
        {
            "id":1,
            "title":"解忧杂货店",
            "content":"《解忧杂货店》是日本作家东野圭吾写作的长篇小说。2011年《小说野性时代》连载，于2012年3月由角川书店发行单行本",
            "img_url":"http://t15.baidu.com/it/u=2090705107,20534764&fm=224&app=112&f=JPEG?w=500&h=500&s=61D0718656561FFFE504A51703000067",
            "add_time":"1984-04-03 11:43:37"}
        ],
        total:50
    }
}
```
















