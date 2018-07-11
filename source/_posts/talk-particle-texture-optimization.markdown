---
layout: post
title: 谈特效贴图优化
subtitle: 没有副标题
date: 2018-05-02 12:00:00
author: 沈从文
header-img: "img/in-post/default-bg.jpg"
categories: "技术文档"
tags:
  - 优化技术
---


# 谈特效贴图优化

> 前言：本来以为有关于贴图压缩应该是常识，但每次最后优化的时候，还是每个项目的特效组，甚至每个人都会问我一遍。于是有此文。  
  以前还写过另外一篇关于特效优化的，主要是效率优化。详见[特效优化篇](/2017/08/24/talk-particles-optimize/)。


# 原则

### 1. 特效贴图的mipmap必须关
![img](/img/in-post/talk-particle-texture-optimization/mipmap.png)<!-- more -->
 
### 2. 原则上必须压缩
![img](/img/in-post/talk-particle-texture-optimization/compression.png)

### 3. 原则上特效贴图尽可能小，256看着不糊就不准用512 

### 4. 没有使用a通道的贴图关闭a通道，或者在ps里去掉
![img](/img/in-post/talk-particle-texture-optimization/a-channel.png)

### 5. 长宽必须使用2的n次幂
![img](/img/in-post/talk-particle-texture-optimization/npot.png)

### 6. 对于透明贴图来说，不透明区域尽可能充满全图
![img](/img/in-post/talk-particle-texture-optimization/fillrate.png)
