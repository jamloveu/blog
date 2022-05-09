---
title: "VUE.js 权威指南 (笔记)"
subtitle: ""
date: 2019-04-15T01:44:44+08:00
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
基于Vue.js 1.0, 部分语法在后续版本已经废除.

# 第一章 遇见Vue.js
## 1.1 MVX模式是什么
MVC/MVP/MVVC
### 1.1.1 MVC
软件架构. Model(模型), Controller(控制器)和View(视图). 
View一般是通过Controller来和Model联系的.基本联系都是单向的.

### 1.1.2 MVP
从MVC演变而来,基本思想有相同之处: Controller/Presenter负责逻辑的处理,Model提供数据,View负责显示.

### 1.1.3 MVVC
相比前两个,MVVC只是把MVC中的 Controller和MVP的Presenter改成了ViewModel.

## 1.2 Vue.js是什么
Vue.js不是一个框架(框架的定义不同,原书是这样说的)--聚焦视图层,构建数据驱动.

1. 轻量
体积小,不依赖其他库
2. 数据绑定
3. 指令
4. 插件化

### 1.2.1 Vue.js与其他库的区别
1. 与AngularJS的区别
    
2. 与React的区别

....


# 第二章 数据绑定
数据绑定是将数据与视图想关联,当数据发生变化时,自动更新视图.
## 2.1语法
### 2.1.1 插值
双大括号`{{  }}` Mustache标签
### 2.1.2 表达式
```
{{ cents/100 }}  //原值的基础上除以100
{{ true? 1 : 0 }}  //值为真,则渲染出1, 否则0

```
### 2.1.3 指令
带`V-`前缀的特殊特性

## 2.2 分割符



# 第三章 指令(Directive)

## 3.1 内部指令

### 3.1.1 v-if
根据表达式的值在DOM中生成或者移除一个元素.

### 3.1.2 v-show
根据表达式的值切换元素的dispaly属性.

### 3.1.3 v-else
必须跟着v-if或者 v-show.
将v-show用于组件时,因为指令的优先级v-else会出问题.所以不要这么做.

### 3.1.4 v-model
用来在`input/select/text/checkbox/radio`等表单控件元素上创建双向数据绑定.

v-model后面可以添加多个参数(number/lazy/debounce)
...

### 3.1.4 v-for
基于数据源重复渲染元素.可以用 `$index`来呈现相应的数据索引.例子:
```
<body id="example">
<ul id="demo">
<li v-for="item in items" class="item-{{ $index }}">
{{ $index }} - {{parentMessage}} {{item.msg}}
</li>
</ul>
</body>
<script>
var demo = new Vue({
    el:'#demo',
    data: {
        items: [
            parentMessage: '滴滴',
            { msg: '滴滴顺风车'},
            {msg: '滴滴专车'}
        ]
    }
})
```

效果:
```
<li class-0> 0-滴滴 顺风车 </li>
<li class-1> 1-滴滴 专车 </li>
```

观察数组变化的变异方法,它们能够触发视图更新.
```
1. push()
2. pop()
3. shift()
4. unshift()
5. splice()
6. sort()
7. reverse()
```


如果想要重复一个包含多个DOM元素的块,可以使用`<template>`标签来包装重复片段.
例子:
```
<ul>
<template v-for="list in lists">
<li> {{list.msg}} </li>
<li class="divider"> </li>
</template>
</ul>
```

也可以使用v-for便利一个对象,每个重复的实例都有一个特殊的属性`$key`,或者给对象的键值提供一个别名.

```
<li v-for="vaule in lists"> {{$key}} : {{value}}
或者
<li v-for="(key,item) in lists2">{{key}} ;; {{item.msg}}

lists={
    w:'didi',
    e:'fe',
    r: '4'
}

lists2={
    one: {msg: 'hello'},
    two: {msg: 'didi fe'}
}
```
效果:
```
w : diid
e: fe
r: 4
或者
one: hello
two: didi fe
```
注意: ES5无法检测到新属性添加到一个对象上或者在对象中删除.
Vue增加了三种方法: 
```
$add(key,value)
$set(key,value)
$deleted(key)
```



###  3.1.6 v-text
key更新元素的textContent

### 3.1.7 v-html
key更新元素的innerHTML,内容按普通HTML插入--数据绑定会忽略

### 3.1.8 v-bind
用于响应更新HTML特性,将一个或多个attribute,或者一个组件prop动态绑定到表达式.

### 3.1.9 v-on 
用于绑定事件监听器; 使用在普通元素上,只能监听原生DOM事件;使用在自定义元素组件时,也可以监听子组件触发的自定义事件.

v-on 后面还可以添加修饰符
1. .stop
2. .prevent
3. .capture
4. .self
5. .{keyCode|keyAlias }
## 

