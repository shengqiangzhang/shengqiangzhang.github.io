---
mathjax: true
mathjax_autoNumber: true
layout: article
title: dual graph对偶图
tags:
    - Deep Learning
---

dual graph指的是对偶图。每一个平面图$G$ ，都有一个对应的对偶图$G^\*$

$G^\*$的定义如下：

1.  $G^\*$ 中的每个点对应$G$中的一个面
2.  对于$G$ 中的每一条边$e$：
    * $e$属于两个面$f1$，$f2$，加入边$({f_1}^\*, {f_2}^\*)$
    * e只属于一个面f，加入回边$(f^\*, f^\*)$

![](http://39.106.118.77/wp-content/uploads/2020/01/f378c8e2be89df01fe111ff439e0ceb5.png)

（图中加入了个绿色边围成的面，需要删除 $s^\* , t^\* $ 之间的边）