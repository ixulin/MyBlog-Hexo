---
layout: post
title: 场景效果及机制列表-第二篇
subtitle: 持续填坑中...
date: 2017-06-08 12:00:00
author: 弗洛伊德
header-img: "img/in-post/default-bg.jpg"
categories: "技术文档"
tags:
    - 图形技术
---


# 场景效果及机制列表
# 第二篇
> 前言：[之前整理过了一篇](/2017/06/05/list-shader-scene)，本来放在那篇文章里，但是gif本来就很大，加载太慢了，于是分开了。    
    附上传送门：[第一篇](/2017/06/05/list-shader-scene) [第二篇](/2017/06/08/list-shader-scene-2) [第三篇](/2017/06/13/list-shader-scene-3) [第四篇](/2017/06/14/list-shader-scene-4)
    
## 草
- 草的交互  
    ![img](/img/in-post/list-render-demo/grass-interaction.gif)  <!-- more -->
    
- 草被烧着了  
    ![img](/img/in-post/list-render-demo/grass-burn.gif)  

- 草被燃烧的火球烧着了  
    ![img](/img/in-post/list-render-demo/grass-burn-interaction.gif)  
    
## 顺便说下bloom
因为有燃烧效果，试了一下bloom，效果果然好太多了，所以bloom这东西用好了性价比简直逆天。看到效果不好，在笃定这东西不行之前先想想是不是没有用好。就跟之前在[这篇文章的最后](https://ixulin.github.io/2017/05/03/talk-bake-in-unity/#题外的感悟)说的一样，当然还有其他的方面也会有这种问题，不一一，我说这个事，对事不对人，大家不要多想   
    ![img](/img/in-post/list-render-demo/grass-burn-bloom.png)  
    
    
