---
layout: article
title: epoch、iteration、batch_size的区别
tags:
    - Deep Learning
---

## epoch

一次epoch是指将所有数据训练一遍的次数，epoch所代表的数字是指所有数据被训练的总轮数。

## iteration

进行训练需要的总共的迭代次数。

## batch size

进行一次iteration（迭代）所训练数据的数量。

<!--more-->

## 例子

例如：有49000个数据，计划进行十轮训练，那么epoch=10；一次训练迭代训练100个数据，batchsize=100，训练一轮总共要迭代490次（49000/100=490）。总的iteration=490\*10=4900次。

具体的计算公式为：  
one epoch = numbers of iterations = N = 训练样本的数量/batch_size