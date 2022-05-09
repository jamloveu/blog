---
title: "AJAX详解"
subtitle: ""
date: 2017-04-15T01:48:17+08:00
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

如何发请求？
用 form 可以发请求，但是会刷新页面或新开页面
用 a 可以发 get 请求，但是也会刷新页面或新开页面
用 img 可以发 get 请求，但是只能以图片的形式展示
用 link 可以发 get 请求，但是只能以 CSS、favicon 的形式展示
用 script 可以发 get 请求，但是只能以脚本的形式运行

有没有什么方式可以实现:
get、post、put、delete 请求都行
想以什么形式展示就以什么形式展示

微软的突破
IE 5 率先在 JS 中引入 ActiveX 对象（API），使得 JS 可以直接发起 HTTP 请求。
随后 Mozilla、 Safari、 Opera 也跟进（抄袭）了，取名 XMLHttpRequest，并被纳入 W3C 规范


AJAX
基本概念:
 AJAX = Asynchronous JavaScript and XML（异步的 JavaScript 和 XML）。
 Ajax主要是客户端与服务器交换数据的一种技术，它有2个主要功能：
向服务器发出请求，而不重新加载页面
接受和处理服务器返回的数据





如何发送HTTP请求？
第一步：需要创建一个XMLHttpRequest 对象，它是浏览器和服务器之间数据交换的桥梁。语法:
variable=new XMLHttpRequest();

第二步：使用 XMLHttpRequest 对象的 open() 和 send() 方法将请求发送到服务器。
XMLHttpRequest.open("GET","test1.txt",true);
XMLHttpRequest.send();

两个方法：
open(method,url,async)，规定请求的类型、URL 以及是否异步处理请求。
method：请求的类型；GET 或 POST
url：文件在服务器上的位置
async：true（异步）或 false（同步）

send(string)，将请求发送到服务器。


GET 还是 POST？
与 POST 相比，GET 更简单也更快，并且在大部分情况下都能用。
然而，在以下情况中，请使用 POST 请求：
无法使用缓存文件（更新服务器上的文件或数据库） 
向服务器发送大量数据（POST 没有数据量限制） 
发送包含未知字符的用户输入时，POST 比 GET 更稳定也更可靠

服务器响应
        如需获得来自服务器的响应，请使用 XMLHttpRequest 对象的 responseText 或 responseXML 属性。
responseText：获得字符串形式的响应数据。
responseXML：获得 XML 形式的响应数据。


处理服务器响应
在处理服务器返回的数据之前，我们首先要知道服务器处理请求的状态（是已经返回数据还是处理出错了）。
        XMLHttpRequest 对象的readyState属性，就是用来标识当前XMLHttpRequest对象处于什么状态的。它有5个状态，如下：
                                  值 状态 描述
0 UNSENT 未初始化状态：此时，已经创建了一个XMLHttpRequest对象
1 OPENED  准备发送状态：此时，已经调用了XMLHttpRequest对象的open方法，并且XMLHttpRequest对象已经准备好将一个请求发送到服务器端
2 HEADERS_RECEIVED 已经发送状态：此时，已经通过send方法把一个请求发送到服务器端，但是还没有收到一个响应
3 LOADING 正在接收状态：此时，已经接收到HTTP响应头部信息，但是消息体部分还没有完全接收到
4 DONE 完成响应状态：此时，已经完成了HTTP响应的接收

if (httpRequest.readyState === 4) {
  // 一切都很好，收到回复
} else {
  // 还没准备好
}

接下来我们就要根据服务器不同的响应执行不同的任务。每当 readyState 改变时，会触发 onreadystatechange 事件。onreadystatechange事件存储函数（或函数名），每当 readyState 属性改变时，就会调用该函数。
最后，我们还要检查HTTP服务器响应的响应代码，status表示响应的HTTP状态码，它也是XMLHttpRequest对象的一个属性。
 status的状态码可以在网上找到，如200表示请求成功.
状态码 响应类别 原因短语
1XX 信息性状态码（Informational） 服务器正在处理请求
2XX 成功状态码（Success） 请求已正常处理完毕
3XX 重定向状态码（Redirection） 需要进行额外操作以完成请求
4XX 客户端错误状态码（Client Error） 客户端原因导致服务器无法处理请求
5XX 服务器错误状态码（Server Error） 服务器原因导致处理请求出错

if (httpRequest.status === 200) {
  // 完美!
} else {
  // 有一个问题的请求
  //例如响应可能包含404（找不到）
  //或500（内部服务器错误）响应代码
}


现在，在检查请求的状态和响应的HTTP状态代码后，您可以根据需要对服务器发送给您的数据进行任何操作
在 onreadystatechange 事件中，我们规定当服务器响应已做好被处理的准备时所执行的任务。

XMLHttpRequest.onreadystatechange=function() ｛
  if (httpRequest.readyState === 4 && httpRequest.status === 200) {
    // 要执行的任务 
  } 
｝


如何使用 XMLHttpRequest? 代码:
myButton.addEventListener('click', (e)=>{
  let request = new XMLHttpRequest()
  request.open('get', '/xxx') // 配置request
  request.send()
  request.onreadystatechange = ()=>{
    if(request.readyState === 4){
      console.log('请求响应都完毕了')
      console.log(request.status)
      if(request.status >= 200 && request.status < 300){
        console.log('说明请求成功')
        console.log(typeof request.responseText)
        console.log(request.responseText)
        let string = request.responseText
        // 把符合 JSON 语法的字符串
        // 转换成 JS 对应的值
        let object = window.JSON.parse(string) 
        // JSON.parse 是浏览器提供的
        console.log(typeof object)
        console.log(object)
        console.log('object.note')
        console.log(object.note)

      }else if(request.status >= 400){
        console.log('说明请求失败') 
      }

    }
  }
})
// 后端代码
  }else if(path==='/xxx'){
    response.statusCode = 200
    response.setHeader('Content-Type', 'text/json;charset=utf-8')
    response.setHeader('Access-Control-Allow-Origin', 'http://frank.com:8001')
    response.write(`
    {
      "note":{
        "to": "小谷",
        "from": "方方",
        "heading": "打招呼",
        "content": "hi"
      }
    }
    `)
    response.end()


jQuery将这些封装好写成函数 $.ajax()  大大简化了ajax的使用, 并且提高了兼容性,
使用实例:

   function drugRecover(drugId) {
            var recoverUrl= "${ctx.contextPath}/drug/drugRecover";
            $.ajax({
                type: 'POST',
                url: recoverUrl,
                dataType: 'json',
                data: {
                    drugId: drugId
                }
            }).done(function (res) {
                //console.log(res);
                // 重新获取页面数据
                var curPageNo = tblContent.find('ul.pagination li.active').attr("yy_page");
                getData(curPageNo);
                //item.prop("disabled", false);
                $('#yy_Modal').modal('hide');

            }).fail(function () {
                alert("fail");
            }); // end ajax
        }