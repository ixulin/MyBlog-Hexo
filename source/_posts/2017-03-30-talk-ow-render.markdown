---
layout: post
title: 谈守望先锋渲染
subtitle: 暴雪爸爸就是叼
date: 2017-03-30 12:00:00
author: 龙胤空
header-img: "img/in-post/default-bg.jpg"
tags:
    - 图形技术
---


# 谈守望先锋渲染

## 拟合

这一段时间看完了PBR，正好以前找了守望先锋的资源，以前尝试过，最早还用Blinn-Phong测试过，当然效果不好。最近看完了PBL、IBL，对于光照，以及物理渲染的理解越来越深刻了，于是重新再尝试用Standard来拟合OW的人物渲染。

拿到守望先锋的图之后，目测推测了通道的作用，R是金属度，G是光滑度。但是用Unity的Standard怎么调都达不到效果，不是某些地方太黑，就是部分地方质感差异。折腾了一天多。也做了很多猜测和拟合的尝试，比如金属度 = R \* G，光滑度 = G \* 1.5 等等，但是效果都不是很好，而且很难适应不同的环境。

后来在睡觉的时候忽然想起来是否是跟色彩空间有关系，第二天来一试果然是。(所以堆时间作用真不大，有时候就是靠思路和灵感。) 自此，对于线性空间和Gamma空间的理解更加深刻了。于是更加认同“**简单属于上帝，复杂属于魔鬼**”，作为暴雪爸爸来说不可能用金属度 = R \* G的，这样太复杂了，对美术来说也是。

放上几张图，我跟游戏对比过，在我测试的光照环境下，拟合度超过了95%。

- **Tracer**  
![img](/img/in-post/talk-ow-render/ow-tracer.jpg)   

![img](/img/in-post/talk-ow-render/ow-tracer-true.jpg) 


- **Genji**  
![img](/img/in-post/talk-ow-render/ow-genji.jpg)  

![img](/img/in-post/talk-ow-render/ow-genji-true.jpg)  


  
- **Bastion**  
![img](/img/in-post/talk-ow-render/ow-bastion.jpg)  


- **Mercy**  
![img](/img/in-post/talk-ow-render/ow-mercy.jpg)


## 一些问题
目前解决了基本材质的拟合，接下来还有皮肤渲染，头发渲染，还有比如眼睛，眼镜等等细节。皮肤基本就是[对SSS的模拟](/2017/xx/xx/talk-skin-render)(先挖坑)，头发的话需要用[各项异性](/2017/xx/xx/talk-hair-render)(先挖坑)。

还有一个是对于金属度的理解，金属度的大小实际上是对于固有色和高光色，以及IBL的调整，在这一点上，Unity的Standard在对indirectSpecular的计算时乘上了specularColor，这样当金属度很低，光泽度很高时很难得到很明显的环境反射，这一点可以修改以适应更有特点的环境反射。

守望先锋虽然使用了PBR的渲染流程，但出图依然走的是手绘风格，暴雪爸爸对手绘是真爱，以前我也说过[手绘的好处](/2017/03/03/talk-npr/)，但依然说服不了美术。

