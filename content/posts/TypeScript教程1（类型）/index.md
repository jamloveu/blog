---
title: "TypeScript教程1（类型）"
subtitle: ""
date: 2022-04-18T21:54:53+08:00
draft: false
author: "Jam"
authorLink: ""
description: ""
keywords: ""
license: ""
comment: false
weight: 0

tags:
- TypeScript
categories:
- TypeScript

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

## 一、基本类型
### 类型声明
- 类型声明是TS非常重要的一个特点
- 通过类型声明可以指定TS变量（参数、形参）的类型
- 指定类型后，当为变量赋值时，TS编辑器会自动检查值是否符合类型声明，符合则赋值，否则报错
- 简而言之，类型声明给变量设置了类型，使得变量只能储存某种类型的值
- 语法：
```
let 变量:类型

let 变量：类型 = 值

function fn(参数:类型, 参数:类型):类型{

}

// 注意：最后面的类型是函数返回值的类型。

```
### 自动类型判断
- TS拥有自动的类型判断机制
- 当对变量的声明和赋值是同时进行的，可以省略掉类型声明
- 类型：


| 类型 | 例子 | 描述 |
| :------------ | :---------- | :------------ |
| number | 1，-2，2.5  | 任意数字|
| string | 'hi' | 任意字符串 |
| boolead | true，false | 布尔值true或者false |
| 字面量 | 其本身 | 限制变量的值就是该字面量的值 |
| any | * | 任意类型 |
| unknown | * | 类型安全的any |
| void | 空值（undefiend） | 没有值（或者undefined） |
| never | 没有值 | 不能是任何值（用的少） |
| object | {name:"jam"} | 任意的JS对象 (一般不使用) |
| array | [1,2,3,4] | 任意的JS数组 |
| tuple | [4,5] | 元组，TS新增类型，固定长度数组 |
| enum | enum{A,B} | 枚举，TS中新增类型 | 


- 可以使用 | 来连接多个类型
- any 表示的任意类型，一个变量设置类型为any后相当于对该变量关闭了TS的类型检测，使用TS中，不建议使用any类型
- 声明变量如果不指定类型，则TS解析器会自动判断变量的类型为any（隐式的bug）
- 类型是any，它可以赋值给任意变量（可以污染其他的变量的类型），但是unknown不会
- unknown 实际上就是一个类型安全的any，unknown类型的变量，不能直接赋值给其他变量，需要检查：
```
let e:unknown;
e = 10
e = 'hello'
e = true

let s:strinmg

//如果赋值需要这样：
if(typeof e ==='string'){
  s = e
}

// 或者用类型断言
s = e as string
s = <string>e

/*
*
* 语法：
* 1. 变量 as 类型
* 2. <类型>变量
*
*/
```
- void 用来表示为空，以函数为例，就表示没有返回值的函数
-  对象一般这样用：
```
let a: object
a = {}
a = function(){}

//这样不会报错...

let b:{
  name: string,
  age?: number
}

b = { name:"jam" }
//加了?后表示属性为可选属性

let c = { name:string }
c = { name: 'jam', a:1,b:2 }

//这样会报错，总不能把所有的属性都写下来吧，可以这样写：

//表示可以有任意属性
let d = { name:string,[propName:string]:any }
d = { name: 'jam', a:1,b:2 }
```
- 如何定义一个函数，指定参数的类型和返回值？【设置函数结构的类型声明，语法：(形参: 类型, 形参: 类型 ...)=> 返回值】
```
let c = (a:number,b:number)=>number
c = function(n1:number, n2:number):number{
  return n1 + n2
}

```
- 数组的语法： 类型[] 或者 Array<类型>
```
// string[] 表示字符串数组
let e: string[]
e = ['a','b','c']

let f = number[] 表示数值数组
或者
let f1 = Array<number>

f = [1,13,3,4]
```
- 元组：固定长度的数组 
```
let h:[string,string]
// 只能写两个且类型必须是string
h =['aa','bbb']
```
- enum 枚举

```
let i:{ name:string, gender: 0 | 1 }
i = {
  name: '孙悟空',
  gender: 1
}

// 上面的0,1虽然可行，但是不能明确它对应的含义,此时就可以用enum:

enum Gender{
  Male,
  Female
}
// 也可以指定值：
enum Gender{
  Male = 0,
  Female = 1
}

let i1:{ name:string, gender: Gender }
i = {
  name: '孙悟空',
  gender: Gender.Male
}


console.log(i.gender === Gender.Male)
```
- & 表示同时：
```
let j:{ name: string } & { age:number }
j = { name:'jam', age:18 }
```

- 类型的别名：
```
type myType = 1 | 2 | 3 | 4 | 5
let k = 1 | 2 | 3 | 4 | 5
let k1 = myType

```
