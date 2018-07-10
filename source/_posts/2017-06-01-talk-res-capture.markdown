---
layout: post
title: 抓取游戏资源流程梳理
subtitle: 在抓资源的路上越走越远
date: 2017-06-01 12:00:00
author: szh
header-img: "img/in-post/default-bg.jpg"
tags:
    - 解决方案
---

# 抓取游戏资源流程梳理


版本 | 更新时间 | 更新内容
---|---|---|---
*1.00* | *2017.05.31* | *初版建档*
*1.01* | *2017.06.05* | *补充：ios资源路径*


## 前言
- *本文系统整理了如何使用Unity Studio工具对游戏（==Android 或 IOS==）资源提取流程，提高提取游戏效率，以便于参考借鉴。*
- *提取到的资源：*
    - ***FBX***
    - ***Font***
    - ***Mesh（.obj格式）***
    - ***Shader***
    - ***TextAsset***
    - ***Texture2D***
    - ***...***
    
- *本文以《崩坏3》游戏资源的提取为例。*

## 准备工作
- *要提取的《崩坏3》游戏apk（或ipa）文件；*
- *提取工具 - Unity.Studio.v0.7.0。*
    - [==*下载地址,密码：jbqu*==](http://pan.baidu.com/s/1bpMpeVX)
    - *下载工具并解压到本地，如图所示*

        ![](https://raw.githubusercontent.com/shaozhonghui/Tools/master/DocPics/ResourcesExtractor/001.png)


## 提取流程
- **寻找《崩坏3》资源所在路径**

    - ***资源所在路径***
        - ***==Android==***
            - ***Apk中***
                - *手动将apk文件的后缀名改为".zip"或".rar"后解压在本地*
            
                    ![](https://raw.githubusercontent.com/shaozhonghui/Tools/master/DocPics/ResourcesExtractor/002.png)

                - *“\assets\bin\Data”*
            
                    ![](https://raw.githubusercontent.com/shaozhonghui/Tools/master/DocPics/ResourcesExtractor/003.png)
            
            - ***手机内存中*** 
         
                - *"/Android/data/com.YourGamePackageName/files/Resources/AssetBundle/"*
               
                    *==例如《王者荣耀》资源路径:==*
               
                    *"==/Android/data/com.tencent.tmgp.sgame/files/Resources/AssetBundle/=="*
               
                    ![](https://raw.githubusercontent.com/shaozhonghui/Tools/master/DocPics/ResourcesExtractor/004.png)
        
        - ***==IPhone==***
            - *手动将ipa文件的后缀名改为".zip"或".rar"后解压在本地*
            
                ![](https://raw.githubusercontent.com/shaozhonghui/Tools/master/DocPics/ResourcesExtractor/009.png)

            - *“\Payload\XXX.app\Data”*
            
                ![](https://raw.githubusercontent.com/shaozhonghui/Tools/master/DocPics/ResourcesExtractor/009_1.png)
     - ***==本示例《崩坏3》资源主要放在APK中assets路径中==***    
        
- **使用UnityStudio工具提取资源**
    - ***打开UnityStudio工具***
        - *在解压后的工具路径中找到“UnityStudio.exe”，点击打开工具* 
        
    - ***工具主要功能介绍，如图所示***
    
        - ![](https://raw.githubusercontent.com/shaozhonghui/Tools/master/DocPics/ResourcesExtractor/005.png) 
        
        - ![](https://raw.githubusercontent.com/shaozhonghui/Tools/master/DocPics/ResourcesExtractor/005_1.png)
        
        - ![](https://raw.githubusercontent.com/shaozhonghui/Tools/master/DocPics/ResourcesExtractor/005_2.png)
    
    - ***向工具中导入游戏资源***
        - *点击"File/Load File",导入要解析的资源文件（==本示例选择第一个格式==）*
        
            ![](https://raw.githubusercontent.com/shaozhonghui/Tools/master/DocPics/ResourcesExtractor/006.png)
        - *导入中*
        
            ![](https://raw.githubusercontent.com/shaozhonghui/Tools/master/DocPics/ResourcesExtractor/006_1.png)
        - *导入完毕*
        
            - ![](https://raw.githubusercontent.com/shaozhonghui/Tools/master/DocPics/ResourcesExtractor/006_2.png)
        
            - ![](https://raw.githubusercontent.com/shaozhonghui/Tools/master/DocPics/ResourcesExtractor/006_3.png)

    - ***导出资源***
        - *点击”Export/All 3D objects(split)“导出Fbx资源*
        - *点击“Export/All assets”导出所有资源（==此时导出mesh资源为.obj资源==）*
        - *如图所示*
        
            ![](https://raw.githubusercontent.com/shaozhonghui/Tools/master/DocPics/ResourcesExtractor/007.png)
            
    - ***浏览提取到的资源***
        - *==Fbx资源==*
        
            ![](https://raw.githubusercontent.com/shaozhonghui/Tools/master/DocPics/ResourcesExtractor/008.png)
            
        - *==Font资源==*
        
            ![](https://raw.githubusercontent.com/shaozhonghui/Tools/master/DocPics/ResourcesExtractor/008_1.png)
            
        - *==Mesh资源==*
        
            ![](https://raw.githubusercontent.com/shaozhonghui/Tools/master/DocPics/ResourcesExtractor/008_2.png)
            
        - *==Shader资源==*
        
            ![](https://raw.githubusercontent.com/shaozhonghui/Tools/master/DocPics/ResourcesExtractor/008_3.png)
            
        - *==TextAsset资源==*
        
            ![](https://raw.githubusercontent.com/shaozhonghui/Tools/master/DocPics/ResourcesExtractor/008_4.png)
            
        - *==Texture2D资源==*
        
            ![](https://raw.githubusercontent.com/shaozhonghui/Tools/master/DocPics/ResourcesExtractor/008_5.png)
            