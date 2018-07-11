---
layout: post
title: 谈特效优化
subtitle: 持续填坑中...
date: 2017-08-24 12:00:00
author: 王国维
header-img: "img/in-post/default-bg.jpg"
categories: "技术文档"
tags:
  - 优化技术
---


# 谈特效优化

> 优化系列传送门：[特效优化篇](/2017/08/24/talk-particles-optimize/)　[场景优化篇之效率优化](/2018/09/28/talk-scene-optimize) [场景优化篇之james](/2017/07/05/talk-scene-optimize-james/) [场景优化篇之lightmap面积优化](/2017/05/03/talk-bake-in-unity/) [动作优化篇](/2017/06/06/talk-game-animation/)

> 前言：一直以来，几乎所有的时间以来，特效都是性能优化的老大难问题。也出于自己太是门外汉，而且很多特效优化的技巧，除了可以通过shader做的，大量的特效优化需要很巧妙的利用mesh的uv和贴图，所以没法入坑，水太深。正巧有能人加入，再有一些之前的积累，于是重新梳理，尽量完善的说到特效优化的各方面，之后如果有新的点也会继续更新。感谢lx，szh，wzq对此做出的贡献。  

> 二更：添加细节说明和截图，2018年6月26日。

## 问题
擒贼先擒王，当然走来要搞清楚问题在哪，也就是说为什么要优化特效。特效之所以费，究其原因，最重要是两点，其一Drawcall，其二像素填充率。  
- **Drawcall**在渲染中不管是透明还是不透明，都是一个很重要的权衡标准，这个Drawcall的优化应该基本都知道，也很明显易懂，**少用或者共用材质求**就可以了。详情原理可以参考[场景优化](/2018/09/28/talk-scene-optimize)里的Drawcall优化。   
- 再一个就是**屏幕填充率**，这个需要细细解释一下，屏幕填充率就是指**当前帧所渲染的像素的个数**。那大家会很有疑问，我屏幕就是1280\*720的啊，也就92w像素，也就是说按道理来说我把每个像素都渲染一遍，屏幕上应该就没有黑的地方了，就不需要渲染了对吧？对没错，但这是最好的情况，实际上，作为手游来说填充率能做到**3倍以内**就算已经不错了。为什么会达到3x的填充率，这就要说到透明的问题了，透明的问题就是在于透明的物体的渲染不会管你现在这个像素有没有被渲染，而依然被渲染的，也就是说**透明的区域叠了多少层就要渲染多少层**。这就是透明通道费的主要原因。  
![img](/img/in-post/talk-particle-optimize/overdraw.gif)  


## 解决方案

## Drawcall及其优化
#### 1. 通过合并贴图、共用材质减少drawcall
原理：Unity粒子系统会进行**动态合并**，也就是2个particle system分别发射出来的面片，只要用的是**同一种材质**，大部分情况下，是可以合并成一个drawcall提交给GPU的。  

错误做法：  
![img](/img/in-post/talk-particle-optimize/combine-texture.png)  
正确做法：  
![img](/img/in-post/talk-particle-optimize/combine-texture-right.png)  
效果：  
![img](/img/in-post/talk-particle-optimize/dynamic-batching.png)  
    
#### 2. 特殊不能进行动态合并的解决方案  
原理：Unity的动态合并有2个缺点。  
第一，顶点信息（包括顶点位置信息，uv，法线等等）数量超过300不会进行动态合并，此外粒子系统更加严格，发射自定义mesh，哪怕这个mesh就是一个quad也不能进行合并。  
第二，就是同时渲染多个材质球导致夹层的问题，可以通过手动设置Sorting Layer和Order in Layer控制。  

正确做法：**尽量使用billboard代替mesh、如果需要手动控制sort相关参数**   
    ![img](/img/in-post/talk-particle-optimize/use-billboard-and-sort.png)  


## 填充率及其优化
#### 1. 在游戏视角下，是否看的见，是否明显


#### 2. 层数的优化，用单层复杂代替多层简单  
- 错误做法1：叠加只为了增加亮度，并不能提高特效本身的视觉丰富性（易错的地方：glow等辉光、火焰、部分刀光）  
![img](/img/in-post/talk-particle-optimize/additive-to-brighter.gif)  
- 错误做法2：叠加只为了少出一张贴图（不常见，但是不能忍）  
![img](/img/in-post/talk-particle-optimize/additive-to-newtex.gif)  

#### 3. 用shader来提高特效丰富性，而不是单纯通过复制particle system的发射  
- 通过shader来合并相似的两层粒子
- 通过uv移动扭曲来丰富效果
- 通过溶解来丰富效果
- 以需求为导向

#### 4. 美术制作方法的优化
- 相同材质球通过粒子系统变形成为不同效果
- 扭曲mesh的uv达到更好的随机效果以丰富单层粒子
- 通过mesh的uv的控制来达到uv动画的节奏感
- 通过恰当的使用mesh来代替大量的点状粒子发射（参考火影大招）

## 贴图的优化
很多贴图没必要复制出来加颜色，或者复制出来加a通道，最好通过shader来做，把颜色和所需要的计算放到材质求上来进行。  
- 错误做法1：贴图只是颜色不一样  
![img](/img/in-post/talk-particle-optimize/same-texture-diff-color.gif)  
- 错误做法2：rgb通道是白的，或者a通道与rgb通道完全一样都可以通过shader来做，不需要浪费  
![img](/img/in-post/talk-particle-optimize/same-texture-diff-a-or-rgb.gif)  

## 基本规范
#### 1. 绝对规范
- 不允许贴图一式两份，添加贴图前先看看有没有一样或者类似的，别想啥加啥，特效组长要担起责任  
![img](/img/in-post/talk-particle-optimize/same-texture.png)  
- 不允许mesh一式两份，同贴图  
- 贴图透明区域过大，导致渲染利用不充分，使填充率上涨（对于透明贴图来说，不透明区域尽可能充满全图；对于additive材质来说黑色区域尽量小）  
![img](/img/in-post/talk-particle-optimize/fill-rate-of-tex.gif)  
![img](/img/in-post/talk-particle-optimize/fill-rate-of-tex.png)  
- 特效贴图的mipmap必须关  
![img](/img/in-post/talk-particle-texture-optimization/mipmap.png)  
- 原则上必须压缩  
![img](/img/in-post/talk-particle-texture-optimization/compression.png)
- 原则上特效贴图尽可能小，256看着不糊就不准用512（先不说纯白贴图的必要性，就拿这张图来说，这个图压倒2*2都不会失真吧，为啥非要用256呢？其他贴图道理一样）  
![img](/img/in-post/talk-particle-optimize/smaller-texture.png)
- 没有使用a通道的贴图关闭a通道，或者在ps里去掉  
![img](/img/in-post/talk-particle-texture-optimization/a-channel.png)
- 长宽必须使用2的n次幂，也就是长宽必须是2、4、8、16、32、64、128、256、512、1024
![img](/img/in-post/talk-particle-texture-optimization/npot.png)
- 不用灯光，不用投影，不用探头  
![img](/img/in-post/talk-particle-optimize/no-high-usage-in-renderer.png)
- 不使用动画（如果需要控制材质球参数来做uv动画等等，请让引擎程序帮你写个能进行uv动画的shader或者通过脚本控制）  
![img](/img/in-post/talk-particle-optimize/no-animator.png)

    
#### 2. 不推荐使用，除特殊情况
- 能用blend就不要用alphablend
- 不使用碰撞
- 不使用子发射器发射粒子
- 不使用躁波
- 不使用触发器
- 不使用拖尾  
![img](/img/in-post/talk-particle-optimize/no-high-usage.png)

### 审校
- 特效的审核，不仅仅是效果的审核，效率以及制作方法也需要审校