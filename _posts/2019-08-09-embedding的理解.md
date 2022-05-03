---
layout: post
title: Embedding的理解
---

Embedding 是一个将离散变量转为连续向量表示的一个方式。在神经网络中，embedding 是非常有用的，因为它不光可以减少离散变量的空间维数，同时还可以有意义的表示该变量。

embedding 有以下 3 个主要目的：

- 在 embedding 空间中查找最近邻，这可以很好的用于根据用户的兴趣来进行推荐；
- 作为监督性学习任务的输入；
- 用于可视化不同离散变量之间的关系。

<!--more-->

One-hot 编码是一种最普通常见的表示离散数据的表示，首先我们计算出需要表示的离散或类别变量的总个数 N，然后对于每个变量，我们就可以用 N-1 个 0 和单个 1 组成的 vector 来表示每个类别。这样做有两个很明显的缺点：

 -    对于具有非常多类型的类别变量，变换后的向量维数过于巨大，且过于稀疏。
 -    映射之间完全独立，并不能表示出不同类别之间的关系。

```python
# One Hot Encoding Categoricals
books = ["War and Peace", "Anna Karenina", 
          "The Hitchhiker's Guide to the Galaxy"]
books_encoded = [[1, 0, 0],
                 [0, 1, 0],
                 [0, 0, 1]]
Similarity (dot product) between First and Second = 0
Similarity (dot product) between Second and Third = 0
Similarity (dot product) between First and Third = 0
```

因此，考虑到这两个问题，表示类别变量的理想解决方案则是我们是否可以通过较少的维度表示出每个类别，并且还可以一定的表现出不同类别变量之间的关系，这也就是 embedding 出现的目的。

```python
# Idealized Representation of Embedding
books = ["War and Peace", "Anna Karenina", 
          "The Hitchhiker's Guide to the Galaxy"]
books_encoded_ideal = [[0.53,  0.85],
                       [0.60,  0.80],
                       [-0.78, -0.62]]
Similarity (dot product) between First and Second = 0.99
Similarity (dot product) between Second and Third = -0.94
Similarity (dot product) between First and Third = -0.97
```

One-hot 编码的最大问题在于其转换不依赖于任何的内在关系，而通过一个监督性学习任务的网络，我们可以通过优化网络的参数和权重来减少 loss 以改善我们的 embedding 表示，loss 越小，则表示最终的向量表示中，越相关的类别，它们的表示越相近。