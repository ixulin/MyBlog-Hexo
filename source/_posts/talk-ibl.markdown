---
layout: post
title: 谈IBL
subtitle: 持续填坑中...
date: 2017-03-15 12:00:00
author: 蔡襄
header-img: "img/in-post/default-bg.jpg"
categories: "技术文档"
tags:
    - 图形技术
---


> 之前在[这里](/2017/03/08/talk-standard/)挖了坑，正好今天没有被项目烦事缠绕，整理完了。主体的思路以及Shader是来自[Marmoset Skyshop](https://www.marmoset.co/skyshop/)，觉得太庞大复杂，简化了一下，采用了Unity内置的Spec Cube，以近似Standard。Marmoset里还扩展了ShaderForge的节点，也很值得学习。

IBL全称是Image Based Lighting，实际上就是做了环境反射，就跟原来反Cubemap做金属效果和水面是一样的，在IBL里稍微不一样的是，为了尽量真实的模拟粗糙表面的环境反射，则需要给Cubemap做一层Blur，在引擎里面为了优化是采用了texCubelod，只需要把Cubemap的lod打开就行了，然后通过Roughness来决定所采lod的层级，这样就可以达到粗糙表面的模糊反射。
<!-- more -->

## 与Standard的对比
大概做了一下对比，如下。左边是IBL实现，Diffuse采用的是Lambert，Specular是Blinnphong。右边是Unity的Standard。

#### Metallic = 0， Smoothness = 1 -> 0
- 光滑
![img](/img/in-post/talk-ibl/ibl-1.jpg)
- 比较光滑
![img](/img/in-post/talk-ibl/ibl-2.jpg)
- 比较粗糙
![img](/img/in-post/talk-ibl/ibl-3.jpg)
- 粗糙
![img](/img/in-post/talk-ibl/ibl-4.jpg)

从图中可以看出，这种拟合方法实际上跟Unity GI没有太大的差别，实际上Unity GI也是这一套。  
区别则是，在完全粗糙的时候，左侧的被渲染球体还是有明显的漫反射，这在对粗糙物体的模拟上，Lambert还是有硬伤，不过以传统光照的出图方法，美术可以通过调整Diffuse贴图来实现。对于Diffuse的更高级的模拟，[以后](https://ixulin.github.io/2017/xx/xx/talk-brdf/)(先挖坑)会在说BRDF的时候说到。(没有比较就没有伤害。)

#### 金属的模拟
![img](/img/in-post/talk-ibl/ibl-metal-simulate.jpg)

对于金属的模拟来说，因为传统光照(Lambert + Blinnphong)没有金属度的概念，只是美术通过漫反射贴图和高光贴图来反应，所以不好对比。但是金属的反射，实际还是相对简单，光滑金属材质的直接漫反射光量通常很小，只要控制好直接高光的光量和环境反射的光量，光滑金属还是很容易模拟的(因为光量守恒)，以前传统的模拟就是通过这种做法。

## 各部分光照的分离
- 直接光照  
> directLihgt = direct Diffuse + direct Specular = Lambert + Blinnphong

![img](/img/in-post/talk-ibl/ibl-lambert-blinnphone.jpg)

- 间接光照  
> indirectLihgt = indirect Diffuse + indirect Specular = SH + IBL \* Fresnel

    - SH
![img](/img/in-post/talk-ibl/ibl-sh.jpg)

    - IBL
![img](/img/in-post/talk-ibl/ibl-indirect-spec.jpg)

- All
![img](/img/in-post/talk-ibl/ibl-all.jpg)

这就是光照的基本构成，TA还是要了解的。以后还会说到AO，以及[AO画法](/2017/xx/xx/talk-ao)(先挖坑)。
