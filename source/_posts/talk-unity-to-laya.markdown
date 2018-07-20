---
layout: post
title: Unity到Laya的注意事项
subtitle: 
date: 2018-05-28 12:00:00
author: 丘吉尔
header-img: "img/in-post/default-bg.jpg"
categories: "技术文档"
tags:
  - 图形技术
---


1. 隐藏物体不支持，会自动显示出来
2. 莫名的部分tga图片自动转换png出错，API只是报错unsupport format，不明原因，用ps转就ok
3. 行走面不带renderer会默认添加renderer
4. ~~目前不确定，应该是不支持unity的2uv展开，得美术自己展lightmap的uv~~
5. 坑不是一般多，导出有时候报错导出失败，不明原因，后来重新执行以下又成功了，擦
6. 导出动作是必须是Generic，humanoid不支持，擦
7. 擦擦擦，导出模型的时候必须把所有东西删干净不然就会导致GetChildAt(0)获取错误
<!-- more -->
8. 从示例库里Copy代码需谨慎，防止有各种看不见的字符导致执行错误
9. ~~莫名其妙的一部分模型变黑，毫无规律，查不出原因，换个用laya的standard替换billnphone就好了，不明原因~~
10. 自己创建物体注意是右手系
11. 场景支持带灯光和相机倒出，如果自己创建注意坐标系
12. 粒子系统里噪声不支持，貌似ColorOverLifetime还不是与时间正比，Limit Velocity不支持。。。
13. 烘焙完成后竟然环境光还加上去了。。。
14. 貌似laya的standard shader不支持lightmap，擦。。。
15. 类里面访问变量一定要加this，否则是默认全局，关键还不报错，特别是name
16. 模型导出注意清空位移，转向，否则会被当做模型内部的数据，位置数据坐标系把x轴翻转就可以
17. 不支持meshcollider
18. 资源路径是/，\不支持，但是不抱错
19. **Typescript：深坑预警，Vector3.ZERO都是引用调用，是同一块内存，不允许使用**
20. Lightmap最好用ps转，不要用laya的工具转，此外应该保证lightmap的颜色在LDR之内
21. Lightmap的shader需要定制修改
22. 动作导入的时候覆盖有时候不会导致重新导入，reimport也不行，得删了重新导才行，莫名其妙




