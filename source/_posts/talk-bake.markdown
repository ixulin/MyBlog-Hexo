---
layout: post
title: 谈烘焙算法哪家强
subtitle: 光照图
date: 2017-04-19 12:00:00
author: 赵佶
header-img: "img/in-post/default-bg.jpg"
categories: "技术文档"
tags:
    - 图形技术
---


曾经美术吐槽过说实时光打出来的效果和烘焙效果差不少，在pc平台上显示的效果和移动平台显示效果也有差别，也一直对Unity的LightMap一知半解，这次测试完了，正好做一下总结。几天前做完的测试，今天终于有时间来写。
<!-- more -->

## 实时光 vs 光照图
这完全就不是一个东西好么？实时光照就是最基本的动态光照，一般就是采用Blin-Phong，也就是说，

> finalColor = baseColor \* ambient + ( baseColor \* diff + specColor \* spec) \* lightColor  

这其中的缺点就是没有全局光照(GI)和环境光遮蔽(AO)，而烘焙的LightMap主要就是为了弥补这两点。

## Beast

## Enlighten

---
> 真心没时间写，再说吧。
