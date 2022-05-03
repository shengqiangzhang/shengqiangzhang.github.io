---
layout: article
title: '笔记: Graph Attention Networks'
---

# Abstract

本文提出一种新颖的 graph attention networks \(GATs\), 可以处理 graph 结构的数据，利用 masked self-attentional layers 来解决基于 graph convolutions 以及他们的预测 的前人方法（prior methods）的不足。

**对象**: graph-structured data.

**方法**: masked self-attentional layers.

**目标**: to address the shortcomings of prior methods based on graph convolutions or their approximations.

**具体方法**: By stacking layers in which nodes are able to attend over their neghborhood's feature. We enables specifying different weights to different nodes in a neighborhood, without requiring any kinds of costly matrix operation or depending on knowing the graph structure upfront.

<!--more-->

# Introduction

图神经网络网络（GNN）首次出现于 Gori 等人（2005）与 Scarselli 等人（2009）的论文，把它作为递归神经网络的泛化形式，能够直接处理更普遍的图类，比如循环图、有向和无向的图。GNN 包括一个迭代过程，来传播节点状态直到平衡；然后是一个神经网络，基于其状态为每个节点生成一个输出；之后，这种思路被 Li 等人（2016）采用并改进，提出在传播步骤中使用门控循环单元（Cho et al.,2014\)。

图注意网络（graph attention networks，GATs），这是一种新型的神经网络架构，用于处理图结构化的数据（graph-structured data），利用隐藏的自注意层克服了过去的基于图卷积或其近似的方法的缺点。这些层的节点可以注意近邻节点的特征，通过将这些层堆叠起来，我们可以为不同节点的近邻指定不同的权重，而不需要耗费任何繁重的矩阵计算（比如矩阵求逆），也不需要预先知道图的结构。通过这种方法，我们同时解决了多个基于频谱的图神经网络的关键挑战，并准备将模型应用于归纳问题以及直推问题。

因此，把卷积泛化到图域中一直是个引发研究者兴趣的课题。在这个方面的进步通常可被归类为光谱方法与非光谱方法。

在这篇论文中，作者们提出了一种基于注意机制的架构，能够完成图结构数据的节点分类。**该方法的思路是通过注意其邻位节点，计算图中每个节点的隐藏表征，还带有自注意策略。这种注意架构有多重性质：**

1.  运算高效，因为临近节点对可并行；
2.  可以通过对近邻节点指定任意的权重应用于不同 degree 的图节点；
3.  该模型可以直接应用于归纳学习问题中，其中包括了需要将模型泛化到此前未见的图的任务。

# GAT Architecture

本文所提出 attentional layer 的输入是一组节点特征，\$h = \\lbrace \\vec\{h\}_\{1\}, \\vec\{h\}_\{2\}, ..., \\vec\{h\}_\{n\} \\rbrace , \\vec\{h\}_\{i\} ∈ R\^\{F\}\$

其中，N 是节点的个数，F 是每个节点的特征数。该层产生一组新的节点特征，作为其输出，即：\$h' = \\lbrace \\vec\{h'\}_\{1\}, \\vec\{h'\}_\{2\}, ..., \\vec\{h'\}_\{n\} \\rbrace , \\vec\{h'\}_\{i\} ∈ R\^\{F'\}\$

为了得到充分表达能力，将输入特征转换为高层特征，至少我们需要一个可学习的线性转换（one learnable linear transformation）。为了达到该目标，在初始步骤，一个共享的线性转换，参数化为 weight matrix，\$W ∈ R\^\{F' \\times F\}\$，应用到每一个节点上。我们然后在每一个节点上，进行 self-attention \--- a shared attentional mechanism α：\$R\^\{F'\} \\times R\^\{F'\} → R\$，计算 attention coefficients:

\$\$ e\_\{ij\} = α\(W \\vec\{h\}_\{i\}, W \\vec\{h\}_\{j\}\)\$\$

为了使得这些系数能够适用于不同的节点，我们用softmax function对所有邻居结点j进行归一化：

\$\$ α_\{ij\} = \\frac\{ exp\( \\vec\{e\}_\{ij\}\) \}\{ \\sum\_\{k∈N\_i\}\{exp\( \\vec\{e\}\_\{ik\}\)\} \}\$\$

在我们的实验当中，该 attention 机制 α 是一个 single-layer feedforward neural network，参数化为权重向量\$ \\vec\{a\} ∈ R\^\{ 2\{F'\} \}\$，对其全部展开，用 attention 机制算出来的系数，可以表达为：

\$\$ α_\{ij\} = \\frac\{ exp\( LeakyReLU \(\\vec\{a\}\^\{T\} \[ W \\vec\{h\}_\{i\} || W \\vec\{h\}_\{j\} \]\) \) \}\{ \\sum_\{k∈N\_i\}\{exp\( LeakyReLU \(\\vec\{a\}\^\{T\} \[ W \\vec\{h\}_\{i\} || W \\vec\{h\}_\{k\} \]\) \)\} \}\$\$

可以得到最终的每个节点的输出向量：  
![](http://39.106.118.77/wp-content/uploads/2019/09/2d82440bc2690de1a3b01aad86bf3c6c.png)

为了稳定 self-attention 的学习过程，我们发现将我们的机制拓展到 **multi-head attention** 是有好处的，类似于：Attention is all you need. 特别的，K 个独立的 attention 机制执行公式（4）的转换，然后将其特征进行组合，得到下面的特征输出：  
![](http://39.106.118.77/wp-content/uploads/2019/09/cb9e68d8707dd21964f901e4a56cfc17.png)

示意图：  
![](http://39.106.118.77/wp-content/uploads/2019/09/1cefdeaf650545010fe6b53169b4e2d9.png)