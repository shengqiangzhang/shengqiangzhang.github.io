---
layout: article
title: '论文笔记: Abstract Meaning Representation for Sembanking'
tags:
    - Deep Learning
---

论文链接：<https://amr.isi.edu/a.pdf>

# 定义

1.  与传统树形结构不同，采用单根 有向无环图(single root,DAG graph)结构；
2.  忽略虚词、介词等，忽略词的形态变化(如复数、过去时等)；

3.  在这个DAG图中，叶子结点表示概念，非叶子结点表示虚结点，虚结点到虚结点的边表示概念之间的关系，虚结点到叶子结点表示实例化的过程。

# 例子

the boy wants to go.  
<!--more-->

### graph format

![](http://39.106.118.77/wp-content/uploads/2019/08/2019-08-05-170053.png)

根据上图所示，可以发现，这是一个关于**want**的事件，根结点实例化出**want**，然后**want**的**arg0**为**boy**，arg1为关于**go**的一个事件，可以理解为**boy want go**。

接着分析**go**，**go**的**arg0**也是**boy**。

可以把**arg0**理解为**施事**，把**arg1**理解为**受事**，这样就好理解多了。

所以**want**和**go**的**arg0**都是**boy**，也就是说**boy**充当了2个角色：  
1\. **want-01**的**arg0**  
2\. **go-01**的**arg0**

### ARM format

根据上述的分析，可轻易得出ARM format：

```python
w / want-01
    :arg0 (b / boy)
    :arg1 (g / go)
        :arg0 (/ boy)
```

### logic format

根据graph format，可轻易得出logic format：  
$$  
{\exists}w, b, g: instance(w, want-01) ∧ instance(b, boy) ∧ instance(g, go-01) ∧ arg0(w,b) ∧ arg1(w,g) ∧ arg0(g,b)  
$$