title: 使用Revit和Dynamo进行火灾出口风险评估
date: 2017-04-10 03:25:24
categories: AR
tags: [npm]
comments: true
---
![](http://osej1thz9.bkt.clouddn.com/static/images/122816_2131_fireexitris6.png)


<!-- <img src="http://osej1thz9.bkt.clouddn.com/IMG_20170623_142040-01.jpeg" alt="IMG_20170623_142040-01.jpeg"> -->

<!-- more -->


![](http://osej1thz9.bkt.clouddn.com/static/images/6a00e553e16897883301b7c9046b5a970b-800wi.gif)

# 情况
所使用的模型如下图所示。该脚本需要检测“正常”室出口门与地面4个“紧急出口”门之一之间的最短路线。因此，创建了该级别的房间计划，在这种情况下可以用作“循环”的房间以橙色表示。

![](http://osej1thz9.bkt.clouddn.com/static/images/122816_2131_fireexitris1.png)

![](http://osej1thz9.bkt.clouddn.com/static/images/122816_2131_fireexitris2.png)
# 结果
脚本的结果是创建每个房间出口到最近的紧急出口的撤离路线。在Dynamo这样看起来如下：

![](http://osej1thz9.bkt.clouddn.com/static/images/122816_2131_fireexitris3.png)

![](http://osej1thz9.bkt.clouddn.com/static/images/122816_2131_fireexitris4.png)

当使用Dynamo曲线创建他们的Revit细节线时，这将导致很好的撤离计划，如下图所示。

![](http://osej1thz9.bkt.clouddn.com/static/images/122816_2131_fireexitris5.png)

![](http://osej1thz9.bkt.clouddn.com/static/images/122816_2131_fireexitris6%20%281%29.png)

![](http://osej1thz9.bkt.clouddn.com/static/images/122816_2131_fireexitris6.png)

# 代码地址
https://autodesk.box.com/s/2q9z8ftqcu1uyj30rn9kh9a9n3l6ly1r
