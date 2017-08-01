title: 欧拉方程
date: 2017-07-19 01:25:24
categories: 基础
tags: [线性代数]
comments: true
---

<center>每晚一次的基础复习课程：欧拉方程，数学界最引人注目和神秘的发现之一</center>
![](http://osej1thz9.bkt.clouddn.com/static/images/euler01.png)

<!-- more -->

# 欧拉方程的发现

首先，来看看该指数函数的泰勒级数表示，E 1 X和三角函数，正弦，的sin（x）余弦，COS（x）的。
![](http://osej1thz9.bkt.clouddn.com/static/images/euler02.png)

比较cos（x）+ sin（x）用E 1 X。通知cos（x）+ sin（x）几乎与泰勒系列相同  E 1 X; 系列中的所有术语与标志完全相同。如你所知，指数函数E 1 X随着输入x的增长而呈指数增长。但是，这是什么指数函数具有周期性（振荡）函数来执行，COS（x）的和的sin（x）？

数学家们试图找出指数函数与2个振荡函数之和之间的奇怪关系。最后，Leonhard Euler完成了这个关系，将虚数，我进入上面的泰勒系列; E 1 {IX}而不是E 1 X而cos（x）+ isin（x）不是cos（x）+ sin（x）。

![](http://osej1thz9.bkt.clouddn.com/static/images/euler03.png)

现在，我们找到E 1 {IX}等于cos（x）+ isin（x），这被称为欧拉方程。

# 欧拉方程图

我们知道指数函数E 1 X随x增长而呈指数增长。但是，这个功能是E 1 {IX}什么样的？

以下图像显示了复数指数函数的图复指数函数，e ^ {ix}，通过绘制E 1 {IX}3D复合空间（x-实 - 虚轴）中的泰勒级数。令人惊讶的是，它是螺旋弹簧（线圈）形状，围绕单位圆旋转。并且，当投影到实数（顶视图）和虚数轴（侧视图）时，它成为三角函数，分别是余弦和正弦。

![](http://osej1thz9.bkt.clouddn.com/static/images/euler04.png)

<center>图表</center>

![](http://osej1thz9.bkt.clouddn.com/static/images/euler05.png)

<center>实数部分</center>

![](http://osej1thz9.bkt.clouddn.com/static/images/euler06.png)

<center>虚数部分</center>

复数指数函数的图形表示复指数函数，e ^ {ix}清楚地显示了与三角函数的关系; 实数的复指数函数，e ^ {ix}余数是余弦，虚部的复指数函数，e ^ {ix}正弦函数与二皮弧度的周期。

![](http://osej1thz9.bkt.clouddn.com/static/images/euler07.gif)

这是一个交互式OpenGL应用程序，用于绘制复指数函数，e ^ {ix}3D中的复数指数函数。

# 欧拉方程含义

![](http://osej1thz9.bkt.clouddn.com/static/images/euler08.png)

当图形复指数函数，e ^ {ix}投影到复平面时，该功能复指数函数，e ^ {ix}在单位圆上进行跟踪。这是周期性的功能二皮。

这意味着提高数学常数，例如到虚数的幂九产生具有以弧度表示的角度x的复数。这种极性形式复指数函数，e ^ {ix}对于表示旋转对象或周期信号非常方便，因为它可以仅在单个术语而不是两个术语中表示复平面中的点a + ib。此外，它简化了在乘法中使用的数学，例如。

复杂的指数形式经常用于电气工程和物理学。例如，周期性信号可以表示傅立叶分析中的正弦和余弦函数的和，并且附加到弦的质量的运动也是正弦的。这些正弦函数可以用复数指数形式来代替，以便更简单的计算。

![](http://osej1thz9.bkt.clouddn.com/static/images/euler09.png)

幅度（norm），| z | 的复数是一个标量值，可以通过使用指数和对数定律来重写：

![](http://osej1thz9.bkt.clouddn.com/static/images/euler10.png)

我们可以扩展任何复数的极坐标形式表示。

![](http://osej1thz9.bkt.clouddn.com/static/images/euler11.png)
<center>复数的极坐标形式</center>

# 二维旋转与欧拉方程

两个复数的乘法意味着2D空间中的旋转。
看下图显示复合平面单位圆上的2个复数。 
当我们比较这两个复数时，我们注意到，虚拟指数形式的角度之和等于两个复数的乘积。它告诉我们，乘以通过执行回转与角度Φ。

我们可以把它扩展到任何复数的任何复数。为了以一定角度Φ 旋转复数z = x + iy，我们简单地乘以数字。然后旋转的结果z'变成。

![](http://osej1thz9.bkt.clouddn.com/static/images/euler12.png)

<center>乘法就是旋转</center>

![](http://osej1thz9.bkt.clouddn.com/static/images/euler13.png)

<center>复数的二维旋转</center>

![](http://osej1thz9.bkt.clouddn.com/static/images/euler14.png)

如果我们通过省略重写它作为一个矩阵形式，它就成为我们熟悉的2×2旋转矩阵。 

![](http://osej1thz9.bkt.clouddn.com/static/images/euler15.png)

# 欧拉恒等式

如果我们将该值代入欧拉方程，那么我们得到：
![](http://osej1thz9.bkt.clouddn.com/static/images/euler16.png)

这个方程称为欧拉识别，显示5个基本数学常数之间的联系; 0,1， ，PI，Ë和一世。

对数函数仅针对域x > 0 定义。但是，欧拉标识允许通过将指数转换为对数形式来定义负x的对数：

![](http://osej1thz9.bkt.clouddn.com/static/images/euler17.png)

如果我们替代欧拉方程，那么我们得到：

![](http://osej1thz9.bkt.clouddn.com/static/images/euler18.png)

然后提高双方的权

![](http://osej1thz9.bkt.clouddn.com/static/images/euler19.png)

上面的方程告诉我们，实际上是一个实数（不是虚数）。

# 欧拉方程的证明

这是使用微积分的证明。我们从右边开始，其区别是：

![](http://osej1thz9.bkt.clouddn.com/static/images/euler20.png)

修改上述公式：

![](http://osej1thz9.bkt.clouddn.com/static/images/euler21.png)

将t移动到左侧，然后应用积分： 

![](http://osej1thz9.bkt.clouddn.com/static/images/euler22.png)

要找到常数C，替换x = 0： 

![](http://osej1thz9.bkt.clouddn.com/static/images/euler23.png)

现在我们知道C = 0，所以上面的等式是： 

![](http://osej1thz9.bkt.clouddn.com/static/images/euler24.png)

最后，将此对数形式转换为指数形式： 

![](http://osej1thz9.bkt.clouddn.com/static/images/euler25.png)