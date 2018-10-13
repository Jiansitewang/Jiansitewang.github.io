---
layout:     post
title:      "[JS]个人resume思路总结（草稿）"
subtitle:   ""
date:       2018-10-10
author:     "WaK"
header-img: "img/post-bg-hello.jpg"
tags:
    - JavaScript
    - 学习总结
---

## 点击topNav跳转对应div

如果用锚点的话，因为topNav是positionfixed的，所以锚点跳转过去后，div一部分会被topNav遮住



解决方法

获取topNav中的a标签，遍历，阻止a标签默认跳转动作

 拿到正在点击的a标签

用a.getAttribute('href') 这个不带浏览器解析的结果

拿到这个‘href’

再用document.querySelector(href)拿到当前点击的元素

用offsetTop拿到当前元素对于页面顶部距离

## 点击topNav缓动至对应div

核心思路关键词 

setInterval  来每隔n像素改变元素的当前定位（position  left right 等

```javascript
let n = 25 //一共动多少次
let duration = 500 / n //多少时间动一次
let currentTop = window.scrollY //当前高度
let targetTOp = top -80 //目标高度  top = 当前元素.offsetTop
let distance = (targetTop - currentTop) / n //需要移动的距离
let i = 0
let id = setInterval(()=>{
    if (i===0){
        window.clearInterval(id)
		return
    }
    i = i + 1
    window.scrollTo(0,currentTop + distance * 1) //需要移动至的位置
},duration)
```

![image-20181008182425123](/Users/wangkai/Library/Application Support/typora-user-images/image-20181008182425123.png)



## 滚动当相应的元素时，topNav也高亮对应的部分

核心思路：滚动时哪一个元素离当前元素近

```javascript
let specialTags = document.querySelectorAll('[data-x]')
let minIndex = 0
  for(let i =1;i<specialTags.length; i++){
    //比较距离
    if(Math.abs(specialTags[i].offsetTop - window.scrollY) < Math.abs(specialTags[minIndex].offsetTop - window.scrollY)){
      minIndex = i
    }
  }
  // minIndex 那一项就是里窗口顶部最近的元素
  specialTags[minIndex].classList.remove('offset')
  //拿到对应a标签和a标签的父元素(也就是li)
  let id = specialTags[minIndex].id
  let a = document.querySelector('a[href="#'+ id + '"]')
  let li = a.parentNode
  //光上面不行，因为li的其他兄弟姐妹也会highlight，所以需要去掉其他兄弟姐妹的highlight
  let brothersAndMe = li.parentNode.children
  for(let i=0; i<brothersAndMe.length; i++){
    brothersAndMe[i].classList.remove('highlight')
  }
  li.classList.add('highlight')
}
// 给css添加样式
let liTags = document.querySelectorAll('nav.menu > ul > li')
for(let i=0; i<liTags.length; i++){
  liTags[i].onmouseenter = function(x){
    x.currentTarget.classList.add('active')
  }
  liTags[i].onmouseleave = function(x){
    x.currentTarget.classList.remove('active')
  }
}
```

## 元素自动浮起

给需要浮起的元素设置脱离原始位置的一个类（‘offset’）

获取离顶部最近的元素

去掉这个元素的下沉类



##留言板

重要的坑

当我们要提交我们的留言信息的时候，JS中要监听form的submit事件





