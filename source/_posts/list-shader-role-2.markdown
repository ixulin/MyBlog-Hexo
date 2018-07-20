---
layout: post
title: 角色效果及机制列表-第二篇
subtitle: 持续填坑中...
date: 2017-06-27 12:00:00
author: 商鞅
header-img: "img/in-post/default-bg.jpg"
categories: "技术文档"
tags:
    - 图形技术
---


> 前言：Substance to Unity5，重新梳理了pbr的Shader，简化了Unity的Standard shader，动图有点大，于是重开一个文章来写。  
> 传送门：[第一篇](/2017/06/05/list-shader-role)[第二篇](/2017/06/27/list-shader-role-2)
<!-- more -->

## 基于物理的渲染
- 以前测试过守望先锋的人物渲染，[文章请戳此处](/2017/03/30/talk-ow-render/)。  
- 后来为了尝试pbr开发流程，尝试过用PS来做（感谢**@徐利利**同学），只不过因为PS里渲染器与U3D里还是有不少差别的，所以效果不是很好，并且开发流程有些繁琐。再后来发现Substance Painter，于是随便涂了一个。图中右边是我在Substance Painter里瞎图的，只是为了表达材质，然后左边是导出到Unity3d渲染出来的。    
![img](/img/in-post/list-render-demo/substance-pbr.png)

- 去参加Unity大会，发现Substance真的已经不是高端工具了，已经是标配了。替美术感到压力好大。

- 另外附上[Substance能做到的效果](https://www.allegorithmic.com/blog/meet-mat-3d-painting-contest-and-winners-are)，这是一个比赛，我还在朋友圈分享过。  
![img](/img/in-post/substance/BartekNowak-6.jpg)


- 这次整理完，具体还没有测效率，因为物件太少了shader效率差异看不太出来。但使用了更简单的计算高光的方法，此外去掉了很多GI没必要的宏，简化了一些效果不明显的GI的计算，优化了部分shader代码，并且扩展了Shader Forge来支持，这样以后可以用很方便的修改和扩展自己的Standard shader，并且测试了一下效果的对比，基本上没有啥区别，也打到手机上看了，更看不太出来。  

- 左边的unity的Standard，右边是简化之后的shader  
    ![img](/img/in-post/list-render-demo/simple-standard.gif)

- 附上我在Substance里面瞎图的小人动图  
    ![img](/img/in-post/list-render-demo/mat-in-substance.gif)

    
    
