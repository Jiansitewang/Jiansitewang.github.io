---
layout:     post
title:      "[Vue]有赞商城vue重构思路（草稿）"
subtitle:   ""
date:       2018-10-14
author:     "WaK"
header-img: "img/post-bg-hello.jpg"
tags:
    - vue
    - 学习总结
---

## 首页-轮播组件

**1、新建一个轮播组件**

1.1	将swiper部分的html拷贝至组件中

1.2	npm安装swiper

> 因为考虑到商品详情页也会用到轮播，所以轮播组件里面就不写data，组件本身只负责展示，数据从别处接收
>
>

**2、数据的获取**

2.1	去index.js的methods中获取轮播图相关的rap数据（模拟）: →api.js  → index.js  

2.2	加载组件



**3、从index.js将数据传递给组件**

> 单vue文件其实就是一个vue实例，在vue文件中，script中会export default 出一个{}（包含很多option）

3.1	子组件：props

> 可以是数组的形式：
>
> ```javascript
> props: ['lists']
> ```
> 也可以是对象的形式:
>
> ```JavaScript
> props:{
>     lists:{
>         option1:xxx,
>         option2:yyy
>     }
> }
> ```

3.2	父类：

V-bind v-if 将数据传给props

> 此时要注意一点，bannerList获取数据的过程是一个异步过程
>
> 在子组件swipe创建（create）的时候，props中的lists是没有数据的
>
> 这时就可以用v-if 当数据传进来时才进行渲染

3.3	拿到lists数据之后就可以给swipe组件中的swiper-slide进行列表渲染v-for

3.4	并绑定a标签的href和img的src

> 数据拿取完毕、渲染操作也做完了，那一个新的问题又摆在了我们面前:
>
> swiper是对dom节点进行操作的，那组件的dom节点是什么时候生成的呢？
>
> 这就要用到生命周期函数了

3.5	在mounted(){}中进行实例化



## 分类页

**1、新建category分页，新建相关html、css、js**

**2、【综合排行】数据的获取和渲染**

2.1	api.js 获取，category.js引入Vue，axios，Foot、实例化

2.2	created中通过methods的一个方法用axios获取数据，

2.3	页面渲染【综合排行】



**3、【二级菜单】数据的获取和渲染**

3.1	一级菜单 click事件 触发数据获取（根据一级菜单id获得不同数据）

3.2	二级菜单中，【综合排行】和其他一级菜单的二级菜单有所不同，所以需要index下标来区分

​	if index==综合排行.index {获取综合排行的二级菜单}

​	else{获取其他二级菜单}

3.3	新增getRank()方法，获取综合排行的二级菜单数据	

3.4	页面渲染

3.5	一级菜单的active类 的添加   （通过比较index和data中设置的默认值）

3.6	通过filter对价格进行处理（加小数点后两位） 







































