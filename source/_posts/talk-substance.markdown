---
layout: post
title: Substance学习心得
subtitle: 持续填坑中...
date: 2017-10-25 12:00:00
author: 刘慈欣
header-img: "img/in-post/default-bg.jpg"
categories: "技术文档"
tags:
  - 图形技术
---


（其实是科普，匿~）  
> 前言：实在忍不了，也特别感兴趣，于是研究了一下substance，上一段时间看的designer，这一周看了painter，折服于substance的设计理念和思路，记录着吧。这个substance是继2dSpine和Live2D之后让我觉得入门很简单，但是要做好太难的软件之一。  
> 说来现在的工具真是越来越方便了，从3dmax到zb到substance都是在解放繁杂工作量的道路上越来越好，不禁为科技的发达和那些大公司的牛逼程序员大神们致敬。


## 最核心的理解
这是我最折服于substance的地方，之前也是在公众号上看到的，觉得特别贴切，道出了substance的设计本质。**“世界上任何最复杂的材质都是有若干个不同的材质叠加出来的”。**比如拿这个复杂的墙体来举例子，实际上就是**红砖，变色的红砖，砖缝中水泥材质，还有磨损的地方**通过若干复杂的遮罩贴图的叠加。<!-- more -->

![img](/img/in-post/talk-substance/substance-desinger-brick.png)

## substance designer和painter的差别
总体说来，designer是做四方连续材质的，也就是做基本材质的，而做好的这些材质可以直接在painter里面用。desinger的基本逻辑是通过可以动态调整参数的mask组件，或者颜色组件，或者材质参数调整组件来组合成最后的效果，跟UE的材质编辑器特别像，不过在节点编辑器里面运算与传输的都是每一步得到的“**图元**”信息。

而在painter里，则是把若干不同的质感叠加就好了（ps.发现ID map真的是好用），也就是**让材质制作的工作完全从设计中解耦**出来，这样设计师**可以更好的把时间放在设计上面**，只用按照自己内心的想法把Mask分好就行了。当然里面也会用到painter笔刷。
![img](/img/in-post/talk-substance/substance-painter-mypaint.png)

## substance desinger心得
记得当时看designer教学视频的时候真的被desinger的思路惊呆了。实际上，desinger这种连线生成材质贴图的系统跟shader节点连线机制有异曲同工之妙，也就是**颜色这个东西，它是一个数值**，你可以用颜色来做各种blend，能用颜色来充当高度图，此外还可以通过随机躁波来增加真实性（因为现实世界真的是随机的），比如**来做磨损，划痕，掉色等等**等等。 

比如像下图里的中间用红圈圈住的图就是通过随机躁波生成出来的中间的图元，后面的整个流程，包括**法线贴图**的计算，**高度图**，**ao图**，**金属度粗糙度图**（其实对于这个材质来说没有），甚至包括**颜色的不同**都是通过这个中间图元叠出来的，这样的话可以让设计师从具体制作的繁杂工作中解耦出来，而**把真正材质制作的核心放在对于材质的理解和拆分上**。
![img](/img/in-post/talk-substance/substance-desinger-cliff.png)

## 关于shader
总体来说substance是为pbr服务的，倒不是说他不能支持自定义的shader，其实是完全ok的，只要把shader按照substance的规则用glsl写好导入就可以了。但是，substance总体说来方便在于我有很多自定义的智能的mask和材质，这样我们可以从材质库里选择材质来调整参数就可以了，如果是自定义shader的话那基本上材质库就需要自己重做，另外如果是npr的shader的话，这种substance带来的优势就没有那么明显了，也就不是特别能提高效率。这是目前的见解。

## 关于感想
这些先进工具真的已经不是高端工具了。捉急。  
以前也说过一篇关于substance painter的，[链接奉上](/2017/06/27/list-shader-role-2/)。

