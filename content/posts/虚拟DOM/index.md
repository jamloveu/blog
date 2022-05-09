---
title: "虚拟DOM"
subtitle: ""
date: 2019-04-15T01:51:58+08:00
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
# 什么是虚拟DOM？
```
/**
 * @author 
 * @description 虚拟 DOM Demo
 * @todo 暂时不考虑复杂情况
 */

class VNode {
  constructor(tag, children, text) {
    this.tag = tag
    this.text = text
    this.children = children
  }

  render() {
    if(this.tag === '#text') {
      return document.createTextNode(this.text)
    }
    let el = document.createElement(this.tag)
    this.children.forEach(vChild => {
      el.appendChild(vChild.render())
    })
    return el
  }
}

function v(tag, children, text) {
  if(typeof children === 'string') {
    text = children
    children = []
  }
  return new VNode(tag, children, text)
}


/*

let nodesData = {
  tag: 'div',
  children: [
    {
      tag: 'p',
      children: [
        {
          tag: 'span',
          children: [
            {
              tag: '#text',
              text: 'xiedaimala.com'
            }
          ]
        }
      ]
    },
    {
      tag: 'span',
        children: [
          {
            tag: '#text',
            text: 'jirengu.com'
          }
        ]
    }
  ]
}

 */


let vNodes = v('div', [
      v('p', [
        v('span', [ v('#text', 'xiedaimala.com') ] )
        ]
      ),
      v('span', [
        v('#text',  'jirengu.com')
        ])
    ]
  )
console.log(vNodes.render())




function patchElement(parent, newVNode, oldVNode, index = 0) {
  if(!oldVNode) {
    parent.appendChild(newVNode.render())
  } else if(!newVNode) {
    parent.removeChild(parent.childNodes[index])
  } else if(newVNode.tag !== oldVNode.tag || newVNode.text !== oldVNode.text) {
    parent.replaceChild(newVNode.render(), parent.childNodes[index])
  }  else {
    for(let i = 0; i < newVNode.children.length || i < oldVNode.children.length; i++) {
      patchElement(parent.childNodes[index], newVNode.children[i], oldVNode.children[i], i)
    }
  }
}



let vNodes1 = v('div', [
      v('p', [
        v('span', [ v('#text', 'xiedaimala.com') ] )
        ]
      ),
      v('span', [
        v('#text',  'jirengu.com')
        ])
    ]
  )

let vNodes2 = v('div', [
      v('p', [
        v('span', [ 
          v('#text', 'xiedaimala.com') 
          ] )
        ]
      ),
      v('span', [
        v('#text',  'jirengu.coms'),
        v('#text',  'ruoyu')
        ])
    ]
  )
const root = document.querySelector('#root')
patchElement(root, vNodes1)

```