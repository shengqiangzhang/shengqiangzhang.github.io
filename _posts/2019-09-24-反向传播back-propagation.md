---
layout: article
title: 反向传播(Back Propagation)
tags:
    - Deep Learning
---

## 什么是BP算法

error BackPropagation算法指的是误差反向传播算法。它是由一个输入层、一个输出层和**一个或多个隐层**构成，它的激活函数采用sigmoid函数，采用BP算法训练的多层前馈神经网络。

## BP算法的基本思想

BP算法全称叫作误差反向传播(error Back Propagation，或者也叫作误差逆传播)算法。其算法基本思想为：在前馈网络中，输入信号经输入层输入，通过隐层计算后由输出层输出，**输出值与标记值比较**，若有误差，将误差反向由输出层向输入层传播，在这个过程中，利用**梯度下降算法**对神经元权值进行调整。

<!--more-->

![](http://39.106.118.77/wp-content/uploads/2019/08/2019-08-01-155557.png)

![](http://39.106.118.77/wp-content/uploads/2019/08/2019-08-01-155743.png)

![](http://39.106.118.77/wp-content/uploads/2019/08/2019-08-01-155847.png)

![](http://39.106.118.77/wp-content/uploads/2019/08/2019-08-01-160001.png)

![](http://39.106.118.77/wp-content/uploads/2019/08/2019-08-01-160043.png)

![](http://39.106.118.77/wp-content/uploads/2019/08/2019-08-01-160117.png)

![](http://39.106.118.77/wp-content/uploads/2019/08/2019-08-01-160155.png)

![](http://39.106.118.77/wp-content/uploads/2019/08/2019-08-01-160232.png)