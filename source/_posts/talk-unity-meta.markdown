---
layout: post
title: Unity项目资源meta规范
subtitle: 最浅显又最容易掉下去的坑
date: 2017-07-05 12:00:00
author: 赵匡胤
header-img: "img/in-post/default-bg.jpg"
categories: "技术文档"
tags:
    - 资源规范
---


# Unity项目资源meta规范

> 前言：这应该是Unity里最浅显又最容易掉下去的坑。给所有的项目都解决过场景丢失材质求，两个同学电脑显示场景不一样，场景莫名Missing Prefab的问题。这些基本都是meta文件漏传，误传导致的，一一列出请知悉。

## 问题
### 1. 场景中MissingPrefab
场景中物件是通过meta文件来定位磁盘上的prefab或者fbx，所以如果出现missing prefab 要么是磁盘上没有这个文件，要么是prefab和fbx的meta文件与场景中物件的prefab的meta文件不匹配。
### 2. 材质丢失等
同理，mat丢失或者meta文件不匹配。其他丢失同理，贴图以及脚本。<!-- more -->

## 解决方案
### 1. 第一次添加文件必须同时提交.meta文件
比如添加了a.fbx，第一次提交fbx时必须同时提交a.fbx.meta。之后的人除了修改了fbx的导入配置参数外不允许再提交.meta文件（防止guid被修改）。
### 2. svn上不允许同时存在同名文件
同名文件大部分原因是因为对svn文件的移动目录操作，比如把a文件从B文件夹移动到C文件夹，如果确实有此需求，则必须把从B文件夹的删除和对C文件夹的添加操作同时提交svn，否则因为meta文件中guid被占用，会造成meta冲突。
### 3. 关于fbx导入材质选项
fbx文件Unity3d会在同级目录下生成Materials文件夹，并生成跟fbx文件名对应的mat（材质）文件，如果有移动材质球文件的需要，则当把.mat文件从自动生成的文件夹中移走的时候，请把fbx导入面板上面的Import Materail（导入材质）选项勾掉，否则当机器重新导入资源时又会生成一堆材质球文件。同样，如果不需要使用导入的材质球，则删除Materials文件夹并取消掉Import Material选项。
### 4. 关于.meta文件的删除
删除文件的svn提交，请同时提交.meta文件的删除。

### 5.移动文件请同时移动meta文件
如题。