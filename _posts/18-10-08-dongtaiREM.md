---
layout:     post
title:      "[css]动态REM（草稿）"
subtitle:   ""
date:       2018-10-08
author:     "WaK"
header-img: "img/post-bg-hello.jpg"
tags:
    - css
    - 学习总结
---
## CSS中常用单位

px 像素

pt 不怎么用 不管

em 一个M的宽度 （因为M的宽高是一致的，其他的字如a,b B 国 等宽高不一定一致）

ex 小写x和数字0的宽度

rem(root em) 根元素的font-size  （***html***）

Vh (viewport height) 视口高度
vw (viewport width) 视口宽度

页面默认font-size是16px

chrome可以自己设置最小字号 默认是12px（设置成6px,显示也是12px）



REM和em其实没啥关系

em = （自己的也就是当前元素所设置的）font-size

REM 是根元素（html）的font-size



百分比布局（高度不好写 没法和宽度做关联）

按比例缩放

REM 既可以按比例缩放，也能将宽度和高度关联起来



REM移动适配方案 核心



rem = font-size = page width



```javascript
var pageWidth = window.innerWidth
document.write = ('<style>html{font-size:' + pageWidth + 'px;}</style>')
```



1rem = html font-size = 1 pageWidth

但这样rem的值会太小（零点几）



就有了以下变形

```javascript
var pageWidth = window.innerWidth
document.write = ('<style>html{font-size:' + pageWidth/10 + 'px;}</style>')
```



字体不要用rem





新的痛点

计算rem很麻烦



