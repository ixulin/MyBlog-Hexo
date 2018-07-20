---
layout: post
title: 自定义Shader Forge
subtitle: 支持开源也支持正版
date: 2017-03-31 12:00:00
author: 公孙乌龙
header-img: "img/in-post/default-bg.jpg"
categories: "技术文档"
tags:
    - 图形技术
---


## Shader Forge

自从去年年中开始了解了Shader Forge之后就觉得Shader Forge是神器，倒不是说他提供的各种功能，毕竟如果你不懂原理，用SF（以下简称）也是连不出来的，你必须对shader了解对非常深刻才能在用SF连节点的时候得心应手。

讲道理，对于开发来说，手写代码和连SF节点其实差不多，因为shader的主要开发主要还是思考过程。至于我为什么非常推荐用SF，以至于能用SF的我就一定用SF，原因在于用SF来写shader会有更少的迭代代价和理解代价。因为SF是通过节点来生成代码的，所以当shader复杂到一定程度的时候，看节点的计算、叠加逻辑比看代码要**直观**很多。<!-- more -->

比如美术3个月之后让你来修改当时的一个shader需求，如果是用代码写的话，而且代码质量风格很糟的情况下，或许需要10-20分钟的理解和回忆时间，但如果是SF的shader的话，我只用把SF打开看下节点的逻辑，这样基本1-3分钟就可以梳理完思路，然后进行扩展和修改，这样效率大大增加了，而且之后还有更好的扩展性。另外如果是手写Shader的话，很多功能不能重复利用，比如描边，溶解，UV流动，这样就是复制粘贴，我最讨厌就是复制粘贴。还有一个如果是用节点连的话，对于光照、方向、效果的叠加计算会更有**逻辑性**，而不是“**试**”出来的。

## 问题

这时候问题就产生了，因为SF提供的节点是有限的，很多时候我没有办法通过SF来写，于是乎只能先生成一部分，然后在手动改，但是这样下次就不能通过SF打开了。比如我很长时间之内都想加的随机功能，这个效果其实很多地方都能用的上，还有比如Marmoset的[Skyshop](https://www.marmoset.co/skyshop/)中用到的IBL，我这个有很大的思路是来自于他，因为在研究它的时候发现他竟然能自定义SF的节点，然后就顺藤摸瓜在SF的dll里看到这个。

![img](/img/in-post/talk-sf-self-def/sf-skyshop.jpg)
这两位作者认识！

于是我也加了一个。
![img](/img/in-post/talk-sf-self-def/sf-orca-rand.jpg)

最后在SF的使用就像这样。
![img](/img/in-post/talk-sf-self-def/sf-self-def-node.jpg)

出来的结果是这样。
![img](/img/in-post/talk-sf-self-def/sf-rand-node.gif)

## 方法
以上是用法，我是反编译的sf的dll来实现的，曾经想过用Mono Cecil来dll注入注册代码实现，不是很熟悉于是放弃了。需要源码的可以给我发邮件。不过说起来很奇怪，我是支持开源的，但还是希望支持正版，毕竟都不容易。现在用的SF还是盗版的，回头买一个。。。

