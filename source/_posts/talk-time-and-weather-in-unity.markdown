---
layout: post
title: 谈Unity里天气和时间效果实现
subtitle: Shape Of My Heart
date: 2018-01-11 12:00:00
author: 周公瑾
header-img: "img/in-post/default-bg.jpg"
categories: "技术文档"
tags:
  - 图形技术
---


# 谈Unity里天气和时间效果实现

> 前言：不知觉忽然写文章就是2018开头了。满怀希望又略显伤感。足立当下，不忘初心。

## 机制
其实天气的各种shader很早很早就有了，一来美术没有用，二来也懒得去总体融合起来。时间系统呢，以前是通过Projector机制来做的，也就是把以人物为中心的圆形区域照亮，其他地方压黑，再配合一些补充的假光，使夜晚氛围出来。这些具体的机制以前的文章里都说了，有需求回去翻下以前的文章。

## 实现
近来说要加时间的切换，也记得以前剑侠是通过lightmap的方法实现的，一来切换光照图其实要比上述说的Projector作假的的方法好，二来我们最近烘焙lightmap的水平比之前还是好多了，所以想着把这一套做出来。于是有此文。<!-- more -->

其实跟技术有关的没有太难的地方，就是代码切换材质还有一些小细节的地方还是挺恶心的，另外因为静态合并的问题，lightmap的uvtilingoffset没法传进去，所以要默认带一套lightmap进场景，这个的结果是会导致内存变大，但似乎没有什么好办法。

最早我的做法是把两套光照图都动态传进去，后来发现除了上面说的原因之外还很难在美术使用的shader上做兼容，因为美术平时使用总不能老要切换制作shader和运行shader，于是还是用默认一套Unity的lightmap，然后传一份晚上的贴图进去，最后代码如下。而且这种方法对扩展shaderforge代码很好兼容改动特别小。  

![img](/img/in-post/talk-time-and-weather-in-unity/lightmap-code.png)

## 演示

![img](/img/in-post/talk-time-and-weather-in-unity/bleach-time-and-weather.gif)


![img](/img/in-post/talk-time-and-weather-in-unity/bleach-day.png)

![img](/img/in-post/talk-time-and-weather-in-unity/bleach-night.png)


![img](/img/in-post/talk-time-and-weather-in-unity/bleach-day-rain.png)

![img](/img/in-post/talk-time-and-weather-in-unity/bleach-night-rain.png)


![img](/img/in-post/talk-time-and-weather-in-unity/bleach-day-snow.png)

![img](/img/in-post/talk-time-and-weather-in-unity/bleach-night-snow.png)


