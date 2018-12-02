---
title: 基于Hexo和NexT主题的部分博客优化
description: 参考了网上Hexo大约38项的基础优化，对Hexo和NEXT主题进行了几项重要且必要的优化。

---

周末抽了一些零散的时间，参考了[https://zhuanlan.zhihu.com/p/33616481][1] 等Hexo+NexT优化的方法，大体上对Hexo进行了一些优化：
1. 基础和默认的Title、Description、keyword，作为一个SEO博客，这当然是第一步。
2. 侧边栏的作者信息和联系方式，知乎和简书的icon均无法正常显示，只能用默认的icon先凑合一下
3. 站点的favicon与本人网上习惯用的头像统一。做了圆形、方形的PNG处理和图片压缩。
4. 分类、标签、关于作者的左侧菜单栏的开启和基础配置。
5. 设置文章内\<a\>链接为浅蓝色，鼠标悬停后为深蓝色+下划线。
6. 开通了一个LeanCloud的账号，通过这样的BaaS平台提供的数据库和开启主题内置好的插件，为每篇文章增加了阅读次数统计功能。（基于PV）
5. 在底部自动增加版权信息和“本文已结束”的功能一直失败，尚未找到原因。
6. 为站点部署的“页面自动压缩”功能一直失败，尚未找到原因。
6. 顺手跟着配置了一个简单的头像动画效果。
7. 留言板块、搜索功能和RSS等未来都需要添加，暂时不折腾了


另外站点目前整体的加载速度非常慢，还达不到SEO理想的需求。后续需要多方面优化。

---- 
更新：根据[https://www.jianshu.com/p/efbeddc5eb19][2]的方式，解决了版权问题。  

办法是在主题配置文件下,搜索关键字 post\_copyright , enable 改为 true 即可
````\# Declare license on posts    
post_copyright:    
enable: true    
license: CC BY-NC-SA 4.0    
license_url: https://creativecommons.org/licenses/by-nc-sa/4.0/ 
````



[1]:	https://zhuanlan.zhihu.com/p/33616481
[2]:	https://www.jianshu.com/p/efbeddc5eb19