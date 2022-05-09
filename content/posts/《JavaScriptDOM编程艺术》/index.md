---
title: "JavaScript DOM 编程艺术"
subtitle: ""
date: 2019-04-15T01:38:18+08:00
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
毕竟是花钱买的.把这本书过了一遍.

## 第二章 JavaScript语法
### 2.1 准备工作（代码引入）
1. 放到文档中的`<script></script>`标签中
2. `<script src="./demo.js">`标签引入

### 2.2 语法
#### 2.2.1 语句(statement)
...
#### 2.2.2 注释（comment）
1. 单行：`//单行注释 `
2. 多行：
    ```
    /*这是
      多行
      注释*/
    ```
#### 2.2.3 变量（variable）
  ```
  var a = 1;
  ```
把值存入变量的操作称为赋值（assignment）

声明（declare）

变量和其他语法的名字都区分大小写。

不允许变量名中包含空格或者标点符号（美元符号“$”例外）

#### 2.2.4 数据类型
1. 字符串 string
2. 数值 number
3. 布尔值 boolean

#### 2.2.5 数组
数组用一个变量来表示一个值的集合。

数组可以用Array声明
```
var arr = Array(4)
或者
var arr1 = []
```

#### 2.2.6 对象
使用Object
```
var list = Object()
或者
var list1 = {}
```

### 2.3 操作
**算数操作符**

      ```
      =
      +
      -
      *
      /
      ++
      --
      +=
     
      ```
### 2.4 条件语句
**if语句**

    ```
    if(条件){
        代码块
    }
    ```

#### 2.4.1 比较操作符
```
>
<
>=
<=
==
===
```

#### 2.4.2 逻辑操作符
```
逻辑与  &&
逻辑或  ||
逻辑非  !
```

### 2.5 循环语句
if语句无法完成重复性的操作。

#### 2.5.1 while循环
```
while(条件){
    条件为true，代码块重复执行
}
```
类似的 **do...while循环**
```
do{
    代码块
}while(条件)
```
二者的区别在与，do...while循环至少或执行一次，而while循环可能一次也不执行

#### 2.5.2 for 循环
最常见的用途之一是对某个数组里的全体元素进行遍历处理。
 
  ```
  var arr1 = [1,3,5,7]
  for(var i=0;i<arr1.length; i++){
      console.log(arr1[i])
      //打印出来的值是1,3,5,7
  }
  ```
  
### 2.6 函数
函数就是一组允许你在代码里随时调用的语句。

```
function name(arguments) {
    statements
}

arguments 参数
```
为了方便区分，在命名变量的时候用下划线，命名函数时用驼峰命名法。

**变量的作用域（scope）**
 
 全局变量（global scope）
 
 局部变量（local scope）
 
 ### 2.7 对象（object）
  对象是自包含的数据集合，包含在对象里的数据可以通过两种形式访问——属性（property）和方法（method）,对象就是由一些属性和方法组合在一起而构成的一个数据实体。
  
  #### 2.7.1 内建对象
  数组就是其中一种。使用new关键字去初始化一个数组时，其实就是在创建一个Array对象的新实例。
  其他、Math对象、Data对象
  
  #### 2.7.2 宿主对象（host object）
  不是JavaScript语言本身，而是由运行环境（浏览器）提供的。
  
  
  
  
### 2.8 小结 
```
......
```


##  第三章 DOM

### 3.1 文档：DOM中的“D”
document
### 3.2 对象：DOM中的“O”
object

与某些特定对象相关联的变量被称为这个对象的属性；只能通过某个特定对象去调用的函数被称为这个对象的方法。

1. 用户定义对象（user-defined object）
2. 内建对象(native object) 比如：Array、Math、Data等
3. 宿主对象（host object）由浏览器提供

### 3.3 模型：DOM中的“M”
model（类似：map）

家族树（节点树）用parent（父）、child（子）、sibling（兄弟）等记号来表明关系。

### 3.4 节点（node）
元素节点、文本节点、属性节点

#### 3.4.1 元素节点（element node）
诸如<body>/<div>/<p>/<ul>这样的。

#### 3.4.2 文本节点 （text node）
例如： `<p> 这个内容是文本节点</p>`

#### 3.4.3 属性节点 （attribute node）
例如： `<p title="这是属性节点！">今天天气不错！</p>`

#### 3.4.4 CSS 

#### 3.4.5 获取元素
`typeof()操作符可以告诉操作数的类型，是字符串、数值、函数、布尔值还是对象`
1. **getElementById**
    返回一个与那个有着给定id属性值的元素节点所对应的对象。
    `document.getElementById(id)`
2. **getElementByTagName**
    返回一个对象数组，每个对象分别对应着文档中有着给定标签的一个元素。
    `element.getElementByTagName(tag)`
    可以用for循环把每一项遍历出来。
    允许把一个通配符（*）作为它的参数。
3. **getElementByClassName**
    HTML5新增
    与2相似，返回一个具有相同类名的元素的数组。
    `getElementByClassName(class)`


#### 3.4.6 盘点知识点
1. 一份文档就是一棵节点树
2. 节点分为不同的类型：元素节点、文本节点、属性节点等
3. getElementById将返回一个对象，该对象对应着文档里一个特定的元素节点。
4. getElementByTagName和getElementByClassName 将返回一个对象数组，它们分为对应着文档里一组特定的元素节点
5. 每一个节点都是一个对象。


### 3.5 获取和设置属性

#### 3.5.1 getAttribute
getAttribute是一个函数，他只有一个参数--你打算查询的属性的名字。
 ```
 onject.getAttribute(attribute)
 ```
 和获取元素节点不同，getAttribute不属于document对象，不能通过document对象调用，只能通过元素节点调用。
 
 例如：可以获取p元素的qwe属性
 ```
 <p id="myP" qwe="test">测试！</p>
  var demo = document.getElementById("myP")
 var demo1 = demo.getAttribute("qwe")
 console.log(demo1) //值为test
 ```

#### 3.5.2 setAttribute
允许对属性节点值进行修改,和上面的类似。
`object.setAttribute(attribute,value)`
例如：可以修改p元素的qwe属性
 ```
  <p id="myP" qwe="test">测试！</p>
  var demo = document.getElementById("myP")
  demo.setAttribute("qwe","hahaha")  //修改p元素的qwe属性值为hahaha
  demo.setAttribute("asd","hahaha")  //添加p元素新的属性asd，值为hahaha
  demo.setAttribute("zxc"，"")  //添加新属性zxc，值为空
 ```    

值得注意的是如果该属性存在，setAttribute是进行修改。如果该属性不在，setAttribute是会创建一个新的属性。
  
 

## 第四章 案例研究: JavaScript图片库
 
### 4.1 标记
加id
### 4.2 JavaScript
`setAttribute()` 是"第一级DOM"的组成部分.
### 4.2.1 非DOM解决方案
1. 改变input的value属性,可以用`element.value = "the new value"` 与`element.setAttribute("value","the new value")` 是等价的.
2. 改变图片的src属性,可以用 `placeholder.src = source`
3. ....

### 4.3 应用这个JavaScript函数
添加事件处理函数(event handler)
`<a href="xxxx.png" onclick="showPic(); return false;">`
触发click事件的同时,阻止a标签的默认事件.

### 4.4 对这个函数进行进行拓展
#### 4.4.1 childNodees 属性
在一棵节点树上,childNodes属性可以用来获取任何一个元素的所有子元素,它是一个包含这个元素全部子元素的数组.

`element.childNodes`
#### 4.4.2 nodeType属性
1. 元素节点的nodeType属性值是1
2. 属性节点的nodeType属性值是2
3. 文本节点的nodeType属性值是3

#### 4.4.3 nodeValue 属性
改变一个文本节点的值 `node.nodeValue`
#### 4.4.4firstChild 和 lastChild 属性


## 第五章 最佳实践
1. 平稳退化
2. 结构和行为分离
3. 分离JavaScript代码
4. 性能考虑,尽量少访问DOM和尽量减少标记
5. 合并和放置脚本
6. 压缩脚本


## 第六章 案例研究: 图片库改进版
1. 添加事件处理函数
2. 入口函数: 
```
window.onload = function() {
    firstFunction();
    secondFunction();
}
```
3. 键盘事件
    onkeypress,onkeyup
4. DOM Core 和 HTML-DOM



## 第七章 动态创建标记
### 7.1 一些传统方法
#### 7.1.1 document.write
document对象的write()方法可以方便快捷的将字符串插入到文档里.避免使用.

#### 7.1.2 innerHTML 属性
可以用来读/写某给定元素的HTML内容

###7.2 DOM方法
#### 7.2.1 createElement 方法
创建一个新元素

`document.createElement(nodeName)`

#### 7.2.2 appendChild 方法
`parent.appendChild(child)`

例子:
```
var testdiv = document.getElementById("testdiv")
var para = document.createElement("p")
testdiv.appendChild(para)
```

#### 7.2.3 createTextNode 方法
创建一个文本节点.`document.createTextNode(text)`
例子: `var text = document.createTextNode("hello world")`

#### 7.2.4 一个更复杂的组合
...

### 7.3 重回图片库

#### 7.3.1 在已有元素前面插入新元素 
`insertBefore()`方法,语法:

```
parentElement.insertBefore(newElement,targetElement)
```

#### 7.3.2 在已有元素的后面插入新元素
`insertAfter()?`方法, 很可惜,DOM没有提供这个方法....




### 7.4 Ajax
JavaScript划时代意义的应用

#### 7.4.1 XMLHttpRequest 对象
Ajax的核心就是 XMLHttpRequest 对象


## 第八章 充实文档的内容

### 8.1 不应该做什么
### 8.2 把"不可见" 变成 可见"
### 8.3 内容
...



## 第九章 CSS-DOM
### 9.1 三位一体的网页 
1. 结构层
2. 表现层
3. 行为层


### 9.2 style 属性
可读写,获取时是一个对象,且只能获取内嵌样式.
```
var para = document.getElementById("example");
alert(typeof para.style)
```
#### 9.2.1 获取样式
比如获取颜色color: `element.style.color`

获取font-family: `element.style.fontFamily`

当有减号-时,应该用驼峰命名法代替.不然浏览器不认识,会误以为是减法运算.

减号和加号之类的操作符是保留字,不允许用在函数或者变量的名字里.

这同时意味着不能用在方法和属性的名字里,方法和属性其实就是关联在某个对象上面的函数和变量.


***注意: 只能获取内嵌样式,不能检索在外部CSS文件里声明的样式***

#### 9.2.2 设置样式
```
element.style.property = value
```
例子:
```
var para = document.getElementById("example");
para.style.color = "blank";
```
***style对象的属性的值必须放在引号里,单引号或者双引号均可; ***


### 9.3 何时该用DOM脚本设置样式
通过DOM来设置样式代码可读写很差,可以通过设置class来设置.class写在对应的CSS文件里.

### 9.4 className属性
是一个可读可写属性.

***注意: 通过className属性来设置某个元素的class属性时将替换(而不是追加)该元素原有的class设置***
 
 
 
 
 
 
 ## 第十章 用JavaScript实现动画效果
 ### 10.1 动画基础知识
 #### 10.1.1 位置
 ```
 position属性的合法值: static/fixed/relative/absolute

 ```
 #### 10.1.2 时间 setTimeout
 ```
 设置:
 setTimeout("function",interval)
 
 取消:
 clearTimeout(movement)
 ```
 
 ...
 
 
 ### 10.2 CSS
 
```
overflow属性:四个值,visible/hidden/scroll/auto
1. visible: 不裁剪溢出内容.
2. hidden: 隐藏溢出内容
3. scroll:  类似hidden,但是会有滚动条
4. auto: 高度足够时没有滚动条,不够时自动添加滚动条
```

...


## 第十一章 HTML5








 
 
 
 
 
 
 