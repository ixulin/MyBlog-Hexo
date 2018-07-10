---
layout: post
title: 谈Standard
subtitle: 持续填坑中...
date: 2017-03-08 23:00:00
author: 贝尔尼尼
header-img: "img/in-post/default-bg.jpg"
tags:
    - 图形技术
---


# 谈Standard

前一段时间研究了下跟PBR相关的东西，正好也看了一下Unity的Standard Shader，更多的PBR理解请戳[这里](/2017/xx/xx/talk-brdf/)(先挖坑)。

在没有了解之前总觉得一堆cginc文件很难看，还有很多宏，看明白了感觉还好。稍微剖析一下，一是国内好像没人写过相关文章，二来自己总结一下加深理解。

Standard 按照我的理解，其实分为两个部分，一个是真正的PBL，第二部分是UnityGI。

### 第一部分：PBL
PBR在目前实时渲染领域还是BRDF，也就是双向反射分布函数，带上表面散射的就是BSSRDF，BRDF是BSSRDF的一种特殊情况的近似，因为要做散射计算，所以实时渲染够呛。之前看过一些论文，工作之外时间有限，理解不深，[以后](/2017/xx/xx/talk-brdf/)再说（先挖坑）。

BRDF最重要的是D\*G\*F。具体的情参考*上面PBR的链接*。PBL这一部分在Unity的Standard里是实现在UnityStandardBRDF.cginc里的。  
D、G分别有各种近似，比如GGX，Cook-Torrance等等，这里不细说。Unity里面好像5.4.x之后改成了GGX，之前是NDFBlinnPhong。关键代码在这里：  
![img](/img/in-post/talk-standard/brdf_code.jpg)  
F就是菲涅尔反射。关键代码在这里：  
![img](/img/in-post/talk-standard/fresnel_code.jpg)  

### 第二部分：Unity GI
GI实际上，按照我的理解分为三个部分。
1. SH，球谐光照，关键代码在这里：  
![img](/img/in-post/talk-standard/sh_code.jpg)

2. IBL，基于图像的光照，具体请戳[这里](/2017/03/15/talk-ibl/)（坑已填）。  
在Unity里面叫GlossyEnvirment，关键代码在这里：  
![img](/img/in-post/talk-standard/ibl_code.jpg)


### 第三部分：Lightmap  
虽然Lightmap属于GI但我更愿意独立到第三部分来写。其一个人觉得dynamic lightmap的增益不是很大，性价比较低。第二，包括人物等动态物体不一定需要lightmap。这一部分在移动平台上可以简化。关键代码在这里：  
![img](/img/in-post/talk-standard/lightmap_code.jpg)


## 自己的理解

了解了这么多，就完全可以自己定义自己的光照，比如shader forge就有生成pbl shader的功能，但是他的GI还是Unity的。另外不想用brdf的还可以用BlinnPhong，用BRDF愿意更换D、G函数的可以随便改，不想用dynamic lightmap就可以不用，完全自己写。下面我说一下对于这三方面的理解。

### PBR  
优点：  
- 保能量，能适应各种光照环境。  
- 美术出图（固有色贴图和金属光泽图）有更客观的规则，而不是完全靠美术水平。  
 
缺点：  
- 计算量更大。  
- 美术需要更换制作流水线。  

### GI
与PBR相反，我认为在Unity Standard Shader里，真正让效果好起来的是GI，或者说GI的近似。球谐光照让物体的暗部有更好的照明，并且能根据天光去变化，不至于让暗部那么死。第二IBL能更好的模拟环境光的作用，其一是给暗部补光，另外就是在特定材质上模拟环境光反射。如果只能选一样，相对PBR，我更愿意使用SH + IBL。而且已经[有人](https://www.marmoset.co/skyshop/)是这么用的。

### Fresnel
在PBR还有IBL里都有一项，这一项真的很重要就是菲涅耳反射。这一点在模拟真实方面真的很重要，因为现实中无处不在菲涅耳现象。

## NPR
讲道理，相对写实游戏来说我还是更喜欢[风格化](/2017/03/03/talk-npr/)。

