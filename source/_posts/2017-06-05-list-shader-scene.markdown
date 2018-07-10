---
layout: post
title: 场景效果及机制列表
subtitle: 持续填坑中...
date: 2017-06-05 12:00:00
author: 黄霑
header-img: "img/in-post/default-bg.jpg"
tags:
    - 图形技术
---


# 场景效果及机制列表
> 前言：之前整理过一回，比较乱，重新整理下，也重新做了动图。有些太简单太基础的东西就略过了。以前的文章[请点击此处](/2017/03/06/list-render-demo/)。  

> 二更：更新了地表积水的效果，添加了新的图片效果。于是把阴影拆分出去。  
    附上传送门：[第一篇](/2017/06/05/list-shader-scene) [第二篇](/2017/06/08/list-shader-scene-2) [第三篇](/2017/06/13/list-shader-scene-3) [第四篇](/2017/06/14/list-shader-scene-4)

## 天气
- 下雪天气效果，重写了之前的积雪shader，做了一些优化，从地面比较低洼的地方开始积雪，另外加了一张躁波让效果更自然  
    ![img](/img/in-post/list-render-demo/snow.gif)
    
    
- 下雨地表积水效果，依然是用一张躁波图  
    ![img](/img/in-post/list-render-demo/wet.gif)
    
- 实时的情况下加上高光  
    ![img](/img/in-post/list-render-demo/wet-spec.gif)
    
- 看国外大牛的博客，找到了一张substance desiginer做的图，果然图好，效果就会好很多，去掉了环境反射，增加了白色的菲涅尔反射，同时去掉了躁波图，而通过高度图来进行水面高度的控制，让视觉更趋于真实    
    ![img](/img/in-post/list-render-demo/wet-height-substance.gif)
    

## 水
- 水，朝一个方向流动  
    ![img](/img/in-post/list-render-demo/water.gif)
    
    
- 支持不同流动方向的水  
    ![img](/img/in-post/list-render-demo/water-flow.gif)
    
