---
layout:     post
title:      "[JS]JavaScript-函数基础相关总结(草稿)"
subtitle:   "总结一下函数相关知识"
date:       2018-09-20
author:     "WaK"
header-img: "img/post-bg-hello.jpg"
tags:
    - JavaScript
    - 学习总结
---

## 1、函数声明
#### 1.1函数表达式
这是一个匿名函数
```Javascript
function(){
	return 1
}
```
但我们不能这样写，必须写成
```Javascript
var fn = function(){
    return 1
};
fn.name // fn
```
**注意**
1、如果将上面的匿名函数加上函数名之后，即

```Javascript
var fn2 = function fn3(){
	return 1
};
console.log(fn3)//报错
```
此时的作用域在该函数内,只能console.log(fn2)

同时,此时：

```Javascript
fn2.name // "fn3"
```

3、函数表达式 右边的函数部分结尾要打分号，来表示语句结束（联想var赋值语句)


#### 1.2函数声明
具名函数 
```Javascript
function A(){
	return 1	
} 
```
作用域 全局

#### 1.3箭头函数

箭头函数一定匿名

```javascript
//箭头函数的几种写法

//当函数复杂时
var fn3 = (i,j) => { 
    console.log(1)
    return i+j
}

//当只有一个参数时，参数的括号可以去掉(函数体的花括号和return一起去掉、且函数体只有一句话)
var fn = i => i+1
fn(7) // fn(7)=8

//当有两个参数时(函数体的花括号和return一起去掉、且函数体只有一句话)
var fn2 = (i,j) => i+j
fn(7,8) // fn(7,8)=15


```

#### 1.4构造函数

构造函数的name属性 为"anonymous"

https://www.w3cplus.com/javascript/6-ways-to-declare-javascript-functions.html

https://zhuanlan.zhihu.com/p/37499036

https://wangdoc.com/javascript/types/function.html

https://segmentfault.com/a/1190000005039150

https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions

## 2、词法作用域

方方的视频没看懂

```JavaScript
//考题

var a = 1
function f1(){
    f2.call()
    console.log(a)
    var a = 2
    
    function f2(){
        var a = 3
        console.log(a)
    }
}
f1.call()
console.log(a)
```

问题：最后打印出什么



```javascript
var a = 1
function f1(){
    console.log(a)
    var a = 2
    f4.call()
}
function f4(){
    console.log(a)
}
f1.call
console.log(a)
```

问题：最后打印出什么
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>JS Bin</title>
</head>
<body>
	<ul>
        <li>选项1</li>
        <li>选项2</li>
        <li>选项3</li>
        <li>选项4</li>
        <li>选项5</li>
    </ul>    
</body>
</html>
```

```javascript
var liTags = doucment.querySelectorAll('li')
for (var i=0;i<liTags.length;i++){
    liTags[i].onclick = function(){
        console.log(i)
    }
}
```

一句话：i还是那个i，但值不一定是原来的那个值

问题： 这是打印出什么




## 3、Call Stack

## 4、this & arguments

## 5、Call/applay 

## 6、bind
fn.bind.call(fn,fn的this,1,2,3)
没听懂
## 7、return
## 8、柯里化 (大概了解)
## 9、高阶函数(大概了解)
输入
array.sort
array.forEach()
array.map()
array.filter()
array.reduce()

输出
fn.bind.call(fn,fn的this,1,2,3)
## 10、回调和构造函数
## 11、箭头函数