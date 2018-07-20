---
layout: post
title: 场景效果及机制列表-第三篇
subtitle: 持续填坑中...
date: 2017-06-13 12:00:00
author: 关关
header-img: "img/in-post/default-bg.jpg"
categories: "技术文档"
tags:
    - 图形技术
---



> 前言：传送门  
> [第一篇](/2017/06/05/list-shader-scene) [第二篇](/2017/06/08/list-shader-scene-2) [第三篇](/2017/06/13/list-shader-scene-3) [第四篇](/2017/06/14/list-shader-scene-4)<!-- more -->
    
## 基于高度的地表混合
地表有多重要就不说了，希望引起重视。

- 正常情况下地表的混合就是Lerp，如果混合区域比较大，就会造成交界处模糊不清，给人一种脏的感觉  
    ![img](/img/in-post/list-render-demo/terrain-blend.png)  
    
- 如果美术能更好的出混合贴图，也就是提高混合贴图的对比度（就是尽量避免出现50%混合的地方），是能够提高一些效果的  
    ![img](/img/in-post/list-render-demo/terrain-blend-contrast.png)  
    
- 再就是除了混合图之外，再通过高度图来做一层计算，能达到这个效果  
    ![img](/img/in-post/list-render-demo/terrain-blend-height.png)  

- 完善的叠加效果，如果是旧的做法就是一片糊  
    ![img](/img/in-post/list-render-demo/terrain-height-blend.gif)  
    
## 地表刷子
- 地表刷子，提高硬度的话基本上等同于以前的刷子  
    ![img](/img/in-post/list-render-demo/height-blend-brush-hard.gif) 
    
- 降低刷子硬度，则能够做到沙子会出现在砖块的缝隙里  
    ![img](/img/in-post/list-render-demo/height-blend-brush.gif) 


## 顺便说几句  
之前写第二篇的时候我就在公司内部群里说过，还要继续打个预防针。虽然这些效果都不错，并且是能实现的，但是这些都是建立在**付出更多贴图，更多计算量**的前提下的。  

所以**不要单纯依赖于**这些稍微高级的做法，游戏美术制作也不仅仅是靠这些效果的简单堆叠（包括后效），因为这肯定会带来性能瓶颈。  

游戏的制作是**步步迭代的**，要保证每一步都是好的，然后去迭代，一定要把**基础、通用的**以及**性价比高**的东西用好，比如[更好的贴图风格](/2017/03/03/talk-npr)，更好的贴图制作规范和方法(这个坑先挖了，希望某个美术来帮我填)、[更好的Lightmap的烘焙方法](/2017/05/03/talk-bake-in-unity)，然后再在这个基础之上通过这些高级的shader和机制来达到更好的效果。

所以平时制作的时候为什么要尽量的节省效率，除了适配之外，还有一个就是留有足够的性能空间给这些效果~~[允悲]
    
