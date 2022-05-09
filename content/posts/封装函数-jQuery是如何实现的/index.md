---
title: "封装函数(jQuery是如何实现的)"
subtitle: ""
date: 2018-04-15T01:45:44+08:00
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
### 自己封装两个函数
#### ①获取指定定元素的兄弟元素
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
</head>
<body>
<ul>
 <li id="iteam1">11</li>
 <li id="iteam2">22</li>
 <li id="iteam3">33</li>
 <li id="iteam4">44</li>
 <li id="iteam5">55</li>
</ul>
  <script>
  <!--这就是API-->
    function getSiblings(node){ 
       var allChildren = node.parentNode.children
       
       var array = {
         length: 0
         }
       for(let i=0; i < allChildren.length; i++){
         if( allChildren[i] !== node ){
          array[array.length] = allChildren[i]
          array.length += 1    
            }
        }
        return array
    }
console.log( getSiblings(iteam3) )
  </script>
</body>
</html>
```

控制台打印出来效果图:
```
{0: li#iteam1, 1: li#iteam2, 2: li#iteam4, 3: li#iteam5, length: 4}
0:li#iteam1
1:li#iteam2
2:li#iteam4
3:li#iteam5
length:4
__proto__:Object
```

#### ②给指定元素添加class
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
</head>
<body>
<ul>
 <li id="iteam1">11</li>
 <li id="iteam2">22</li>
 <li id="iteam3">33</li>
 <li id="iteam4">44</li>
 <li id="iteam5">55</li>
</ul>
  <script>
    function addClass(node,classes){
        for(var key in classes){
            var value = classes[key]
            if(value){
                node.classList.add(key)
            }else{
                node.classList.remove(key)
            }
        }
    }
    addClass(iteam3,[a:true,b:false,c:true])
  </script>
</body>
</html>
```
效果如下:
```
...
<li id="iteam3" class="a c">33</li>
...
```


这样我们就可以直接调用这些函数:
```
getSiblings(iteam3)
addClass(iteam3,[a:true,b:false,c:true])
```

#####  起个名字: 命名空间
```
window.jamdom = {}
jamdom.getSiblings =  function (node){ 
       var allChildren = node.parentNode.children
       var array = {
         length: 0
         }
       for(let i=0; i < allChildren.length; i++){
         if( allChildren[i] !== node ){
          array[array.length] = allChildren[i]
          array.length += 1    
            }
        }
        return array
    }
jamdom.addClass = function (node,classes){
        for(var key in classes){
            var value = classes[key]
            if(value){
                node.classList.add(key)
            }else{
                node.classList.remove(key)
            }
        }
    }
```
###### 然后可以这样使用:
```
jamdom.getSiblings()
jamdom.addClass([a:true,b:false,c:true])
```
这就叫命名空间.


但是这种写法不够优雅,我们希望可以这样写:
```
iteam3.getSiblings()
iteam3.addClass([a:true,b:false,c:true])
```

#### 怎么做到呢?
##### 第一种方法: 直接改Node的原型
```
Node.prototype.getSiblings = function (){
    return 1
}

iteam3.getSiblings()
```

完整改一下:
```
Node.prototype.getSiblings = function (){
       var allChildren = this.parentNode.children
       var array = {
         length: 0
         }
       for(let i=0; i < allChildren.length; i++){
         if( allChildren[i] !== this ){
          array[array.length] = allChildren[i]
          array.length += 1    
            }
        }
        return array
}

iteam3.getSiblings()
```
下一个:
```
Node.prototype.addClass = function (classes){
        for(var key in classes){
            var value = classes[key]
            if(value){
                this.classList.add(key)
            }else{
                this.classList.remove(key)
            }
        }
    }

iteam3.addClass([a:true,b:false,c:true])
```
但是,不能直接改原型,可能会出现覆盖问题.

##### 第二种方法: 自己写一个Node2
```
window.Node2 = function (node) {
    return {
        getSiblings: function () {
            var allChildren = node.parentNode.children
            var array = {
                length: 0
            }
            for (let i = 0; i < allChildren.length; i++) {
                if (allChildren[i] !== node) {
                    array[array.length] = allChildren[i]
                    array.length += 1
                }
            }
            return array
        },
        addClass: function(classes){
            for(var key in classes){
                var value = classes[key]
                if(value){
                    node.classList.add(key)
                }else{
                    node.classList.remove(key)
                }
            }
        }
    }
}
var node2 = Node2(iteam3)
node2.getSiblings()
node2.addClass([a:true,b:false,c:true])
```

现在把名字改一下:
```
window.jQuery = function (node) {
    return {
        getSiblings: function () {
            var allChildren = node.parentNode.children
            var array = {
                length: 0
            }
            for (let i = 0; i < allChildren.length; i++) {
                if (allChildren[i] !== node) {
                    array[array.length] = allChildren[i]
                    array.length += 1
                }
            }
            return array
        },
        addClass: function(classes){
            for(var key in classes){
                var value = classes[key]
                if(value){
                    node.classList.add(key)
                }else{
                    node.classList.remove(key)
                }
            }
        }
    }
}
var node2 = jQuery(iteam3)
node2.getSiblings()
```

是不是和jQuery长得很像,其实jQuery的更强大一些,比如我们升级一下jQuery的选择器:
```
window.jQuery = function (nodeOrSelector) {
    let node
    if(typeof nodeOrSelector === "string"){
        node = document.querySelector(nodeOrSelector)
    }else{
        node = nodeOrSelector
    }
    
    return {
        getSiblings: function () {
            var allChildren = node.parentNode.children
            var array = {
                length: 0
            }
            for (let i = 0; i < allChildren.length; i++) {
                if (allChildren[i] !== node) {
                    array[array.length] = allChildren[i]
                    array.length += 1
                }
            }
            return array
        },
        addClass: function(classes){
            for(var key in classes){
                var value = classes[key]
                if(value){
                    node.classList.add(key)
                }else{
                    node.classList.remove(key)
                }
            }
        }
    }
}
var node2 = jQuery("#iteam3")
node2.getSiblings()
```
简单来说:jQuery实际是一个构造函数,接受一个节点,然后返回一个函数去操作这个节点.
