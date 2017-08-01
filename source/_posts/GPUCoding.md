title: 判断点是否在多边形（Polygon）内部
date: 2017-07-27 22:25:24
categories: algorithms
tags: [算法]
comments: true
---

<center>判断点是否在多边形内部，具有普遍的生活化意义，比如坐车去旅行，到达省份交界处，就会有网络运营商发来的提示短信，又比如逛商场中的商家推送信息，这都是其应用，那么就从图形学上分析一下是如何实现的</center>

<!-- more -->


# 如何判断

目前对于点在polygon内部的判断主流有两种方法：

+ 射线法，即以点开始做一射线，计算与多边形边界相交的次数。

+ winding number，多边形围绕点的缠绕次数（原文：which counts the number of times the polygon winds around the point P. The point is outside only when this "winding number" wn = 0; otherwise, the point is inside.）

今天，主要说说第一种射线法：

![](http://osej1thz9.bkt.clouddn.com/static/images/polygon1.png)

任一射线穿过多边形，奇数段位于多边形之内，偶数段位于多边形之外。

从该点出发沿着X轴画一条射线，依次判断该射线与每条边的交点，并统计交点个数，如果交点数为奇数，则在多边形内部（如图3个交点），如果焦点数是偶数，则在外部，射线法对凸和非凸多边形都适用，复杂度为O(N)，其它N是边数。

[源码可参考](http://alienryderflex.com/polygon/)

当多边形数目较少时，我们可以依次遍历每一个多边形（暴力遍历法），然后用射线法进行判断，这样效率也很高。而当多边形数目较多时，比如有10万个多边形，这个时候需要执行10万次射线法，响应时间达到3.9秒，这在互联网应用几乎不可忍受。下表是本人的简单测试，多边形边数均为7。

![](http://osej1thz9.bkt.clouddn.com/static/images/polygon2.png)

# R树索引

暴力遍历法效率低下的原因是与每一个多边形都进行了射线法判断，如果能减少射线法的调用次数性能就能提升。因此我们的优化思路很直接，首先通过粗筛的方法快速找到符合条件的少量多边形，然后对粗筛后的多边形使用射线法判断，这样射线法的执行次数大大降低，效率也能大大提高。怎么粗筛呢？对于一维数据我们常常使用索引的方法，比如通过B树索引找到某一个范围区间段，然后对此范围区间段进行遍历查找，对于二维空间数据常常使用空间索引的方法，比如通过R树找到范围区间内的多边形，然后对此范围内的多边形进行精确判断，下面介绍最常使用的空间索引R树的解决思路。

+ 外包矩形表示多边形

由于多边形形状各异，我们需要以一种统一的方式来对多边形进行近似，最简单的方式就是用最小外包矩形来表示多边形。

![](http://osej1thz9.bkt.clouddn.com/static/images/polygon3.png)

+ 对最小外包矩形建立R树索引

![](http://osej1thz9.bkt.clouddn.com/static/images/polygon4.png)

+ 查询

1. 首先通过R树迅速判断用户所在位置（粗红点）是否被外包矩形覆盖（红色点代表用户所在位置；R树平均查询复杂度为O(Log(N))，N为多边形个数）；
2. 如果不被任何外包矩形覆盖则返回不在地理围栏多边形内;
3. 如果被外包矩形覆盖则还需要进一步判断是否在此外包矩形的多边形内部，采用上文提到的射线法判断

![](http://osej1thz9.bkt.clouddn.com/static/images/polygon5.png)

# 多边形边数较多怎么办

大多数应用的地理围栏多边形都比较简单，但有时也会遇到一些特别复杂的多边形，比如单个多边形的边数就超过十几万条，这时候对此复杂多边形执行一次射线法也非常耗时（因为射线法时间复杂度为O(N)，N为多边形边数）。

如何提高对复杂多边形执行射线法的计算效率呢？同样使用R树索引！笔者在实际应用中对边数较多（如超过1万）的多边形的边再单独进行R树索引，具体如图所示，首先对多边形的每条边构建最小外包矩形，然后在这些最小外包矩形基础上构建R树索引（R树索引上的外包矩形未画出），这样射线法求交点的时候首先通过R树判断射线是否与外包矩形相交，最后对R树粗筛后的边进行精确求交判断，时间复杂度从O(N)降到O(Log(N))，大大提高了计算效率。
	   
![](http://osej1thz9.bkt.clouddn.com/static/images/polygon6.png)

# 实践

autocad有30多万个多边形，通过在内存中构建R树索引，使得线上实时地理围栏查询平均响应时间在1ms以内，而暴力查询响应时间是9秒左右。

# 相关源码

[Python](https://pypi.python.org/pypi/Rtree/)
[Java](http://jsi.sourceforge.net/)
[Javascript](https://github.com/leaflet-extras/RTree)
[C#](http://sourceforge.net/p/cspatialindexrt/code/HEAD/tree/ )