---
title: "HTTP 状态码"
subtitle: ""
date: 2018-03-12T01:00:23+08:00
draft: false
author: "jam"
authorLink: ""
description: ""
keywords: ""
license: ""
comment: false
weight: 0

tags:
- HTTP
- 学习笔记
categories:
- HTTP

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

# 1xx消息
这一类型的状态码，代表请求已被接受，需要继续处理。
## 100 Continue
服务器已经接收到请求头，并且客户端应继续发送请求主体（在需要发送身体的请求的情况下：例如，POST请求），或者如果请求已经完成，忽略这个响应。
## 101 Switching Protocols
服务器已经理解了客户端的请求，并将通过Upgrade消息头通知客户端采用不同的协议来完成这个请求。
## 102 Processing
WebDAV请求可能包含许多涉及文件操作的子请求，需要很长时间才能完成请求。该代码表示​​服务器已经收到并正在处理请求，但无响应可用。


# 2xx成功
这一类型的状态码，代表请求已成功被服务器接收、理解、并接受。
## 200 OK
请求已成功，请求所希望的响应头或数据体将随此响应返回。
## 201 Created
请求已经被实现，而且有一个新的资源已经依据请求的需要而创建，且其URI已经随Location头信息返回。
## 202 Accepted
服务器已接受请求，但尚未处理。最终该请求可能会也可能不会被执行，并且可能在处理发生时被禁止。
## 203 Non-Authoritative Information（自HTTP / 1.1起）
服务器是一个转换代理服务器（transforming proxy，例如网络加速器），以200 OK状态码为起源，但回应了原始响应的修改版本。
## 204 No Content
服务器成功处理了请求，没有返回任何内容。
## 205 Reset Content
服务器成功处理了请求，但没有返回任何内容。与204响应不同，此响应要求请求者重置文档视图。
## 206 Partial Content
服务器已经成功处理了部分GET请求。类似于FlashGet或者迅雷这类的HTTP 下载工具都是使用此类响应实现断点续传或者将一个大文档分解为多个下载段同时下载。


# 3xx重定向
这类状态码代表需要客户端采取进一步的操作才能完成请求。
## 300 Multiple Choices
被请求的资源有一系列可供选择的回馈信息，每个都有自己特定的地址和浏览器驱动的商议信息
## 301 Moved Permanently
被请求的资源已永久移动到新位置，并且将来任何对此资源的引用都应该使用本响应返回的若干个URI之一。

# 4xx客户端错误
这类的状态码代表了客户端看起来可能发生了错误，妨碍了服务器的处理。
## 400 Bad Request
由于明显的客户端错误，服务器不能或不会处理该请求。
## 401 Unauthorized
即用户没有必要的凭据
## 403 Forbidden
服务器已经理解请求，但是拒绝执行它。
## 404 Not Found
请求失败，请求所希望得到的资源未被在服务器上发现


# 5xx服务器错误
表示服务器无法完成明显有效的请求。
## 500 Internal Server Error
通用错误消息，服务器遇到了一个未曾预料的状况，导致了它无法完成对请求的处理。没有给出具体错误信息。
## 501 Not Implemented
服务器不支持当前请求所需要的某个功能。当服务器无法识别请求的方法，并且无法支持其对任何资源的请求。
## 502 Bad Gateway
作为网关或者代理工作的服务器尝试执行请求时，从上游服务器接收到无效的响应。
## 503 Service Unavailable
由于临时的服务器维护或者过载，服务器当前无法处理请求
## 505 HTTP Version Not Supported
服务器不支持，或者拒绝支持在请求中使用的HTTP版本。
## 507 Insufficient Storage
服务器无法存储完成请求所必须的内容。这个状况被认为是临时的。
## 508 Loop Detected 
服务器在处理请求时陷入死循环。 
## 510 Not Extended
获取资源所需要的策略并没有被满足。
## 511 Network Authentication Required
客户端需要进行身份验证才能获得网络访问权限，旨在限制用户群访问特定网络。