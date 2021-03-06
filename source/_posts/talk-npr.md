---
layout: post
title: 谈风格化、NPR游戏设计
subtitle: 持续填坑中...
date: 2017-03-03 12:00:00
author: 王摩诘
header-img: "img/in-post/default-bg.jpg"
categories: "技术文档"
tags:
    - 游戏设计
    - 图形技术
---

> NPR：非写实渲染

### 1.为什么采用风格化设计？
* 风格化效果，视觉冲击
* 风格化、NRP更不容易过时
	* 写实的标准变化快
	* 使用NPR的游戏在多年以后看上去还是很酷
* 写实类游戏有时候太过严肃和黑暗
	* 卡通类游戏更明亮和好玩
* 在强调游戏视觉特性上更自由
	* 比如夸张游戏角色特征 

<!-- more -->

> 部分引用自：[Stylized Rendering In Games](https://s3-ap-southeast-1.amazonaws.com/erbuc/files/42add4c2-73f9-4201-b03f-1d637b8a8145.pdf) by Steven Bouma

* 举例
	* 守望先锋
	* 罪恶装备
	* 塞尔达传说
	- 无主之地

更多风格化游戏梳理，请戳[这里]()(先挖坑)

### 2.美术设计
* 大块的几何设计
	* 剪影  
![img](/img/in-post/talk-npr/jianying.jpg)
	* 灰度梯度  
![img](/img/in-post/talk-npr/huidu.jpg)

> Players of multiplayer combat games such as Team Fortress 2 must be able to visually identify other players very quickly at a variety of distances and viewpoints in order to assess the possible threat. In Team Fortress 2 in particular, the player’s class—Demo, Engineer, Heavy, Medic, Pyro, Spy, Sniper, Soldier or Scout—is extremely important to gameplay and hence the silhouettes of the nine classes were carefully designed to be very distinct from one another, as shown in Figure 2. 
> 
> 翻译：多玩家战斗的游戏中，比如TF2（Dota2，OW），玩家必须以很快的速度，在不同距离和视窗下分辨出对方玩家的角色英雄，以应对可能的攻击威胁。在TF2中，玩家使用的角色英雄类型非常重要，比如爆破兵，工程师，重型装备，军医，喷火兵，间谍，狙击手，士兵，侦察兵，于是我们非常小心的设计了这些角色的剪影以区分于其他不同角色。

* 配色设计
	* 色系  
![img](/img/in-post/talk-npr/owrenwu.jpeg)

> 有关于颜色我现在还不成体系，[以后]()(先挖坑)可能会涉及，可以参考[V社的角色美术参考](https://support.steampowered.com/kb/9334-YDXV-8590/dota-2-workshop-character-art-guide)


* 大块的贴图设计  
![img](/img/in-post/talk-npr/dakuaitietu.jpg)  
	* 暗黑三  
![img](/img/in-post/talk-npr/anheisantietu.jpeg)  
    - 手游剑侠世界  
![img](/img/in-post/talk-npr/jianxiashijie.jpg)  

> Not only does this hand-painted source material create an illustrative NPR style in rendered images, but we have found that these abstract texture designs hold up under magnification better than textures created from photo reference due to their more intentional design and lack of photo artifacts. Furthermore, we believe that high frequency geometric and texture detail found in photorealistic games can often overpower the ability of designers to compose game environments and emphasize gameplay features visually using intentional design choices such as changes in color value.
> 
> 翻译：这种手绘风格的材质不仅能在渲染中产生特征明显的NPR风格，而且我们发现这些抽象的纹理设计比由照片参考创建的纹理，能更好地处理纹理被放大的情况，因为它们更具有有意的设计，并且没有多余的事实细节。 此外，我们相信在写实类游戏的场景环境的设计和视觉特性的强调上，高频率的几何和纹理细节，经常会影响到设计师在使用有意的设计选择上的能力，比如颜色的搭配和使用。

> 两段英文均引用自：[V社的TF2渲染文档](http://www.valvesoftware.com/publications/2007/NPAR07_IllustrativeRenderingInTeamFortress2.pdf)  

从上面看，这种手绘+大块颜色设计的方法被大量的游戏采用，说明确实有很大的好处。实际上如果仔细看，上帝视角游戏会更多的会采用这种方法，因为游戏中物体在屏幕上实际很小，镜头拉近的需求并不多，如果过于细节反而会因为纹理采样产生锯齿。


### 3.渲染设计
* 更明快的视觉
	* 用wrap diffuse取代diffuse
* 颜色强调
	* 阶梯的颜色分布
	* 补色在光照以及阴影中的使用 
		- 用ambient cube取代ambient
		- wrap light
* 轮廓强调
	* 描边
	* 边缘光

> 这一段之后会配上渲染图

### 4.风格化设计中的心理学
人类天生具有抽象能力，也就是在格式塔心理学中的“完形”的能力，于是对于轮廓化，层次化，特征化有更容易的知觉。目前还是不成体系，[以后]()可能会写(先挖坑)。  
之前已经写了一篇关于风格的，不仅仅限于游戏，详情请戳[这里](/2017/03/01/talk-style/)


