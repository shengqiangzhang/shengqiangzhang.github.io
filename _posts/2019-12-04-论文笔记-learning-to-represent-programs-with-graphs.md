---
layout: article
title: '论文笔记: Learning to Represent Programs with Graphs'
---

![](http://39.106.118.77/wp-content/uploads/2019/10/93c52a7a8ec3e01b70ed2e5c9750ff18.png)

```pyhton
(x1, y2) = Foo();
while (x3 > 0)
    x4 = x5 + y6

```

LastUse边：红色，LastWrite边：绿色，ComputeFrom：紫色

一个变量token是能够在语法树叶子结点中出现多次的，上述代码中，x出现4次，y出现2次。

<!--more-->

x4用LastUse边指向x5，说明x4上次用到了x5给他赋值；  
x3用LastUse边指向x4，说明在上次循环结束时，x4被赋值，然后在判断本次循环是否继续的时候，x3的取值就是上次循环的x4；  
x5用LastUse边指向x3，说明在本次循环开始时，x5的取值就是本次循环开始时的x3；  
x3用LastUse边指向x1，说明在第一次进行循环判断条件的时候，x3的取值就是初始化的时候的x1的取值；

x4用LastWrite边指向x4，说明是在自循环，所以x4的上一次写入仍然是x4；  
x4用LastWrite边指向x1，说明在x1刚好被赋值以后，开始的第一次循环的x4的上一次写入是x1；  
x3用LastWrite边指向x1，说明在x1刚好被赋值以后，开始的第一次循环判断的x3的上一次写入是x1；  
x3用LastWrite边指向x4，说明在本次循环结束后，x4被写入，到了下一次循环的时候，x3的上一次写入就是这个x4；  
x5用LastWrite边指向x1，说明在x1刚好被赋值以后，开始的第一次循环的x5的上一次写入是x1；  
x5用LastWrite边指向x4，说明在本次循环结束后，x4被写入，到了下一次循环的时候，x5的上一次写入就是这个x4；

x4用ComputedFrom指向x5和y6，说明x4是由x5和x6赋值得到的。