---
layout: post
title: 角色效果及机制列表-第三篇
subtitle: 持续填坑中...
date: 2017-07-26 12:00:00
author: 龙族世界
header-img: "img/in-post/default-bg.jpg"
categories: "技术文档"
tags:
    - 图形技术
---


> 前言：一些机制，很早之前就弄好了，后来整理抽象成独立的模块到git上，一直没有放过来。跟机制有关的，还差物理击飞没有整理。  
> 传送门：[第一篇](/2017/06/05/list-shader-role)[第二篇](/2017/06/27/list-shader-role-2)[第三篇](/2017/07/26/list-shader-role-3)

## 换装
- 以前在冰火实现过，后来换手游因为效率问题一直没用，以前的也被干掉了，想着以后可能会用，先加上。而且独立出来松耦合，给其他项目接。
<!-- more -->
![img](/img/in-post/list-render-demo/avatar.gif)  


## 物理骨骼
- 不是用的unity的铰链和布料系统，太费，用的是spring bone的机制
![img](/img/in-post/list-render-demo/physic-bone.gif)  


## 物理击飞
- 机制已经支持了，待整理