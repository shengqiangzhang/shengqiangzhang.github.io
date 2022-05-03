---
layout: article
title: tf.variable_scope和tf.name_scope的区别
tags:
    - Deep Learning
---

1.  tf.variable_scope可以让变量有相同的命名，包括tf.get_variable得到的变量，还有tf.Variable的变量

2.  tf.name_scope可以让变量有相同的命名，只是限于tf.Variable的变量

```bash
import tensorflow as tf; 
import numpy as np; 
import matplotlib.pyplot as plt;

with tf.name_scope('V1'):
    # a1 = tf.get_variable(name='a1', shape=[1], initializer=tf.constant_initializer(1))
    a2 = tf.Variable(tf.random_normal(shape=[2,3], mean=0, stddev=1), name='a2')
with tf.name_scope('V2'):
    # a3 = tf.get_variable(name='a1', shape=[1], initializer=tf.constant_initializer(1))
    a4 = tf.Variable(tf.random_normal(shape=[2,3], mean=0, stddev=1), name='a2')

with tf.Session() as sess:
    sess.run(tf.initialize_all_variables())
    # print a1.name
    print a2.name
    # print a3.name
    print a4.name
```