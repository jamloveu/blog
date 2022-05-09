---
title: "前端面试--Vue2"
subtitle: ""
date: 2022-04-16T00:18:04+08:00
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
## Vue2的生命周期钩子有哪些？数据请求放在哪个钩子？
![](images/lifecycle.png)

- vue2文档写的很清楚，红色空心框重的文字皆为生命周期钩子：
1. create x2 （before + ed）
2. mount x2  
3. update x2
4. destroy x2

还有三个写在钩子文档里：
1. activated
2. deactivated
3. errCaptured 一般业务用不到，做组件封装可能会用，错位上报。


请求要放在mounted里面，因为放在其他地方都不合适。

为什么不在create里面用？SSR会执行created。
因为如果用到SSR，后端会执行一次，前端又会执行一次，不符合我们的预期，不应该在后端执行一次。

mount不会在后端执行，只会在前端执行。

为什么不在update中执行？因为update触发的太频繁了，一般请求只请求一次。

为什么不在destory中？组件销毁时不可能。

## Vue2 组件间通信方式有哪些？
1. 父子组件：使用【props和emit事件】进行通信
2. 爷孙组件：
  - a) 使用两次父子组件通信来实现
  - b) 使用依赖注入【provide + inject】来通信
3. 任意组件：使用eventBus = new vue() 来通信
 - a) 主要API是eventBus.$on和eventBus.$emit
 - b) 缺点是事件多了就很乱，难以维护
 4. 任意组件：使用Vuex通信（Vue3可用Pinia代替Vuex）


## Vuex 用过吗？怎么理解？
1. 背下文档的第一句话：Vuex是一个专门为 Vue.js应用程序开发的 状态管理模式+库。（状态管理的库）
2. 说出核心概念的名字和作用：store、State、Getter、Mutation、Action、Module
- store 是一个大容器，带有一个mapState辅助函数
- State 用来读取派生状态，附有一个mapGetters 辅助函数
- Mutation 用于同步提交状态变更，附有一个mapMutation辅助函数
- Action 用于异步变更状态，但它提交的是 mutation，而不是直接变更状态。
Module 用于给store划分模块，方便维护代码。

常见追问：Mutation和Action为什么要分开？
答案：为了让代码更易于维护。（可是Pinia就把Mutation和Action合并了）


## VueRouter 用过吗？怎么理解？
1. 背下文档第一句话：VueRouter是Vue.js的官方路由。它和Vue.js核心深度集成，让用Vue.js构建单页应用变得轻而易举。
2. 说出核心概念的名字和作用：router-link、router-view、嵌套路由、Hash模式和History模式、导航守卫、懒加载
- router-link：点击跳转
- router-view：用来容纳路由的视图
- 嵌套路由：路由加一个children
- 导航守卫：用来通过跳转或取消的方式守卫导航
- 懒加载：`import('xxxx')`

3. 常见追问：
- Hash模式和History模式的区别？a. 一个用的是Hash一个用的是History API。b. 一个不需要后端nginx配合，一个需要（History需要）
- 导航守卫如何实现登录控制？
```
router.beforeEach((to, from, next) => {
  if (to.path === '/login') return next()
  if (to是受控页面 && 没有登录) return next('/login?return_to=' + encodeURIComponent(to.path))
  next()
})
```

推荐阅读：https://blog.csdn.net/sinat_36521655/article/details/106125910


## Vue2 是如何实现双向绑定的？
1. 一般使用 `v-model` 或者 `.sync`(已废弃，合并为v-model)实现，`v-model`是`v-bind:value`和`v-on:input`的语法糖
  - (a) `v-bind:value`实现了data -> UI的单项绑定
  - (b) `v-on:input`实现了UI -> data 的单向绑定
  - (c) 加起来就是双向绑定了。

2. 这两个单向绑定是如何实现的呢？
  - (a) 前者是通过 Object.defineProperty API 给data的每个属性递归的创建getter和setter进行劫持（监听），用来监听data的改变，data一变就会安排改变UI。
  - (b) 后者通过 template compiler 给DOM天剑事件监听，DOM input的值变了就回去修改data。

  推荐阅读：https://www.cnblogs.com/canfoo/p/6891868.html

