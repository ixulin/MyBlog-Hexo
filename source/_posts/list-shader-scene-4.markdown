---
layout: post
title: 场景效果及机制列表-第四篇
subtitle: 持续填坑中...
date: 2017-06-14 12:00:00
author: 乔布斯
header-img: "img/in-post/default-bg.jpg"
categories: "技术文档"
tags:
    - 图形技术
---


> 前言：因为修改了第一篇文章，添加了新的效果，导致第一篇文章太大，于是把第一篇文章拆开了。  
> 附上传送门：[第一篇](/2017/06/05/list-shader-scene) [第二篇](/2017/06/08/list-shader-scene-2) [第三篇](/2017/06/13/list-shader-scene-3) [第四篇](/2017/06/14/list-shader-scene-4)
    
## 投影
- 平面阴影，一种非常便宜的阴影实现方式，网易系游戏大量采用此方法，还能支持点光阴影<!-- more -->
    ![img](/img/in-post/list-render-demo/planar-shadow.jpg)  
    
    ![img](/img/in-post/list-render-demo/planar-shadow.gif)
    
    
- 投影器，重新写了一套，一是为了简化，二来能当插件一样独立使用，并且支持编辑器不运行的情况，底层和LightFace一个机制  
    ![img](/img/in-post/list-render-demo/projector.gif)

    
    

    
