---
layout:     post
title:      "bootstrap3 vs materializecss 颜值当道"
subtitle:   "是时候让你的网站改头换面了"
date:       2016-07-12 12:00:00
author:     "Guolei"
header-img: ""
header-mask: 0.3
catalog:    true
tags:
    - github
---

> bootstrap火了那么多年  materializecss作为后起之秀 能否超越前辈


## 简介

 **materializecss基于Google Material Design的现代化响应式前端框架**

官方号称：

* 提供大量组件样式，实现快速开发
* 用户体验棒，颜值很重要！
* 文档齐全，易用上手快

![](http://www.qinguolei.com/img/in-post/mts/mts-index.jpeg)

[git代码地址](https://github.com/thunderqin/materializecss-demo.git)

## 使用感受

* 样式库非常精美，动效细腻

举例几个自己特别喜欢的效果

![](http://www.qinguolei.com/img/in-post/mts/lei.gif)
![](http://www.qinguolei.com/img/in-post/mts/dx.gif)

* 各个组件完全兼容移动端

**PC**
![](http://www.qinguolei.com/img/in-post/mts/hengpin.jpeg)

**手机**
![](http://www.qinguolei.com/img/in-post/mts/phone.jpeg)

参照了bootstrap 分成12等分，通过 s m g 来设计不同宽度下的占比

![](http://www.qinguolei.com/img/in-post/mts/changdu.jpeg)

比如大屏幕下占一半，小屏幕占三分之一
那么class为  b6 s4

* 大量的组件 涵盖百分之九十的场景

** 样式类 **
![](http://www.qinguolei.com/img/in-post/mts/css.jpeg)

** 组件类**
![](http://www.qinguolei.com/img/in-post/mts/components.jpeg)

** 交互类 **
![](http://www.qinguolei.com/img/in-post/mts/jss.jpeg)

* 使用十分简单，write less do more

大多数组件通过class就可以了

* 样式和交互分离

可以通过js来控制交互 比如下拉菜单

![](http://www.qinguolei.com/img/in-post/mts/jscontrol.jpeg)


## 碰到的问题

* 官方提供的slider 定制型差 移动端体验 很差
[体验地址](http://materializecss.com/fullscreen-slider-demo.html)

* Autocomplete 并不能跑起来 调试的时候 没有走对应的代码


![](http://www.qinguolei.com/img/in-post/mts/autocom.jpeg)


![](http://www.qinguolei.com/img/in-post/mts/jscontrol.jpeg)
提示找不到 autocomplite对象

## 坑

1 组件化固然好，碰到定制化的东西，需要了解内部实现，改起来比较烦
2 并不能很好的结合VUE和REACT。
3 谷歌字体被墙。




