---
title: "什么是JSONP"
subtitle: ""
date: 2018-04-15T01:47:03+08:00
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
先说总结：
**JSONP（JSON with Padding）是数据格式JSON的一种“使用模式”，可以让网页从别的网域要数据。**

在搞明白这些之前，我们先想一个问题？ **局部刷新怎么做？**

有没有想过，不返回 HTML，返回 JS
#### 方案一：用图片造 get 请求
```
button.addEventListener('click', (e)=>{
    let image = document.createElement('img')
    image.src = '/pay'
    image.onload = function(){ // 状态码是 200~299 则表示成功
        alert('成功')
    }
    image.onload = function(){ // 状态码大于等于 400 则表示失败
        alert('失败')
    }
})
```
#### 方案二：用 script 造 get 请求
```
button.addEventListener('click', (e)=>{
    let script = document.createElement('script')
    script.src = '/pay'
    document.body.appendChild(script) //script标签必须插入body中才能发GET请求
    script.onload = function(e){ // 状态码是 200~299 则表示成功
        e.currentTarget.remove()
    }
    script.onload = function(e){ // 状态码大于等于 400 则表示失败
        e.currentTarget.remove()
    }
})

//后端代码
...
if (path === '/pay'){
    let amount = fs.readFileSync('./db', 'utf8')
    amount -= 1
    fs.writeFileSync('./db', amount)
    response.setHeader('Content-Type', 'application/javascript')
    response.write('amount.innerText = ' + amount)
    response.end()
}
...
```
这种技术叫做 SRJ - Server Rendered JavaScript

域名什么的无所谓
跨域 SRJ

确定函数名

JSONP
```
请求方：frank.com 的前端程序员（浏览器）

响应方：jack.com 的后端程序员（服务器）

请求方创建 script，src 指向响应方，同时传一个查询参数 ?callbackName=yyy
响应方根据查询参数callbackName，构造形如
yyy.call(undefined, '你要的数据')
yyy('你要的数据')
这样的响应
浏览器接收到响应，就会执行 yyy.call(undefined, '你要的数据')
那么请求方就知道了他要的数据


这就是 JSONP
```
#### 方案3：JSONP
```
button.addEventListener('click', (e)=>{
    let script = document.createElement('script')
    let functionName = 'frank'+ parseInt(Math.random()*10000000 ,10)
    window[functionName] = function(){  // 每次请求之前搞出一个随机的函数
        amount.innerText = amount.innerText - 0 - 1
    }
    script.src = '/pay?callback=' + functionName
    document.body.appendChild(script)
    script.onload = function(e){ // 状态码是 200~299 则表示成功
        e.currentTarget.remove()
        delete window[functionName] // 请求完了就干掉这个随机函数
    }
    script.onload = function(e){ // 状态码大于等于 400 则表示失败
        e.currentTarget.remove()
        delete window[functionName] // 请求完了就干掉这个随机函数
    }
})

//后端代码
...
if (path === '/pay'){
    let amount = fs.readFileSync('./db', 'utf8')
    amount -= 1
    fs.writeFileSync('./db', amount)
    let callbackName = query.callback
    response.setHeader('Content-Type', 'application/javascript')
    response.write(`
        ${callbackName}.call(undefined, 'success')
    `)
    response.end()
}
...

约定：
callbackName -> callback
yyy -> 随机数 frank12312312312321325()

jQuery中可以这样写：
 $.ajax({
 url: "http://jack.com:8002/pay",
 dataType: "jsonp",
 success: function( response ) {
     if(response === 'success'){
     amount.innerText = amount.innerText - 1
     }
 }
 })
```

###  Q：JSONP 为什么不支持 POST？

因为JSONP是通过动态创建script标签来实现的，而script标签只能发GET请求，不能发POST请求。

相关链接：http://www.cnblogs.com/dowinning/archive/2012/04/19/json-jsonp-jquery.html
