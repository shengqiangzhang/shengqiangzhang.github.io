---
layout: article
title: '论文笔记: Abstract Meaning Representation for Sembanking'
tags:
    - Deep Learning
---

## Abstract

希望一个简单，整句，语义结构的 **词库** 可以刺激统计自然语言理解和生成方面的新工作，例如宾州树库鼓励统计分析的工作。 本文概述了AMR及其相关工具。

## Introduction

1.  手工进行语义注释是不合理的，因为我们为命名实体，共同引用，语义关系，语篇连接词，时间实体等提供了单独的注释，但是每个注释都有其自己的关联评估，并且训练数据分散在许多资源中。
2.  我们缺乏简单易读的英语句子的句库，以及它们的整个句子，逻辑含义。
3.  AMR设计基本准则
    * AMR是一个有标签的、有根的图，便于人们阅读和程序遍历。
    * AMR旨在抽象化语法特性
    * AMR与我们可能想如何从字符串中得出含义无关，反之亦然。 在将句子翻译成AMR时，我们不会规定规则应用程序的特定顺序，也不会提供反映此类规则序列的对齐方式。 这使得sembanking非常快，并且使研究人员可以探索自己的想法，了解字符串与含义之间的关系。
    * AMR主要针对英语

在一篇50页的注释指南中已经对AMR进行了描述，在本文中，主要是对AMR进行高度描述，并且提供一个软件工具来评估。

## AMR Format

1.  单根，有向，边标签，叶标签的图

## AMR Content

1.  "b / boy" 表示用一个实例b来表示概念boy
2.  “\(d / die-01 :location \(p / park\)\)” means there was a death \(d\) in the park \(p\)
3.  AMR uses approximately 100 relations:
    * Frame arguments, following PropBank con- ventions. :arg0, :arg1, :arg2, :arg3, :arg4, :arg5.
    * General semantic relations. :accompanier, :age, :beneficiary, :cause, :compared- to, :concession, :condition, :consist-of, :de- gree, :destination, :direction, :domain, :dura- tion, :employed-by, :example, :extent, :fre- quency, :instrument, :li, :location, :manner, :medium, :mod, :mode, :name, :part, :path, :po- larity, :poss, :purpose, :source, :subevent, :sub- set, :time, :topic, :value.
    * Relations for quantities. :quant, :unit, :scale.
    * Relations for date-entities. :day, :month, :year, :weekday, :time, :timezone, :quarter, :dayperiod, :season, :year2, :decade, :century, :calendar, :era.
    * Relations for lists. :op1, :op2, :op3, :op4, :op5, :op6, :op7, :op8, :op9, :op10.

<!--more-->

![](http://39.106.118.77/wp-content/uploads/2020/01/7729a95f64647c43b42a1776c48351d3.png)

## Example

在阅读例子之前，读者可以参考AMR阅读指南。

1.  Frame arguments. For example, the frameset “describe-01” has three pre-defined slots \(:arg0 is the describer, :arg1 is the thing described, and :arg2 is what it is being described as\).  
    ![](http://39.106.118.77/wp-content/uploads/2020/01/d3f0b04cfc7bfd84fe0310cf10cdd815.png)
2.  General semantic relations. AMR also includes many non-core relations, such as :beneficiary, :time, and :destination.  
    ![](http://39.106.118.77/wp-content/uploads/2020/01/5738ee2854383ae66387b82c8338fd0a.png)

3.  Co-reference.

4.  Inverse relations. We obtain rooted structures by using inverse relations like :arg0-of and :quant-of.  
    ![](http://39.106.118.77/wp-content/uploads/2020/01/67ba797ede9d9d835420fe6d13cf5a9f.png)  
    ![](http://39.106.118.77/wp-content/uploads/2020/01/80d309a2c597f60e3ac035affb3e9178.png)

5.  Modals and negation. AMR represents negation logically with :polarity, and it expresses modals with concepts.  
    ![](http://39.106.118.77/wp-content/uploads/2020/01/4290fe1b13b9729bbc57586c7397a5ce.png)  
    ![](http://39.106.118.77/wp-content/uploads/2020/01/6c301ef01c7ab90eec2d941569da237f.png)  
    ![](http://39.106.118.77/wp-content/uploads/2020/01/4cbc49321a0f6112724044d4c4b802e5.png)

6.  Questions. AMR uses the concept “amr- unknown”, in place, to indicate wh-questions.  
    ![](http://39.106.118.77/wp-content/uploads/2020/01/f0dd10906f14448742fcc29d22b8005b.png)

7.  后面还有很多…………

## Limitations of AMR

1.  AMR不代表屈折形态学的时态和数字，它省略冠词。这加快了注释的过程。我们没有针对这些现象的良好语义目标表示。一个轻量级的语法样式表示可以通过一个自动的后处理分层。
2.  AMR没有通用量词。 诸如“全部”之类的词会修饰其头部概念。 AMR不会区分真实事件和假设事件，未来事件或想象的事件。 例如，在“男孩想去”中，即使“ go-01”可能发生也可能不发生，“ want-01”和“ go-01”的实例具有相同的状态。
3.  We represent “history teacher” nicely as “\(p / per- son :arg0-of \(t / teach-01 :arg1 \(h / history\)\)\)”. How- ever, “history professor” becomes “\(p / professor :mod \(h / history\)\)”, because “profess-01” is not an appropriate frame. It would be reasonable in such cases to use a NomBank \(Meyers et al., 2004\) noun frame with appropriate slots.

## Creating AMRs

我们已经开发了强大的AMR编辑器，可通过Web界面访问。AMR编辑器允许通过文本命令和图形按钮快速，增量地构造AMR。 它包括有关关系，数量，版本等的在线文档，并带有完整的示例。 用户登录，编辑器记录AMR活动。 编辑器还提供了重要的指南，旨在提高注释器的一致性。 例如，警告用户有关不正确的关系，断开的AMR，带有PropBank框架的单词等。用户还可以在现有的sembank中搜索短语，以查看过去的处理方式。 编辑器还允许并排比较来自不同用户的AMR，以进行培训。

## Current AMR Bank

当前，这篇论文有一个由数千个句子组成的手动构建的**AMR库**，其中的一个子集可以免费下载，其余的则通过LDC目录分发。  
在最初开发AMR时，作者建立了以下AMR：  
\+ 225 short sentences for tutorial purposes  
\+ 142 sentences of newswire \(_\)  
\+ 100 sentences of web data \(_\)

而LDC 提供以下AMR:

* 1546 sentences from the novel “The Little Prince”
* 1328 sentences of web data
* 1110 sentences of web data \(\*\)
* 926 sentences from Xinhua news \(\*\)
* 214 sentences from CCTV broadcast conversation \(\*\)

Collections marked with a star \(\*\) are also in the OntoNotes corpus

## Relate Work

如今，从事全句语义分析的研究人员通常使用像GeoQuery这样的小型特定领域的sembank。对规模更大，覆盖面广的sembank的需求使得多个项目得到了建立，其中包括……

## Future Work

1.  Sembanking  
    我们的主要目标是继续进行扩充sembanking。我们想雇用一个大型的sembank来创建用于自然语言理解和生成的共享任务。 这些任务可能还会引起人们对图和字符串之间概率映射的理论框架的兴趣。

2.  Applications  
    首先，我们正在探索统计NLU和NLG在基于语义的机器翻译（MT）系统中的使用。 在该系统中，我们使用AMR注释中英文双语数据，然后训练组件以将中文映射到AMR，并将AMR映射到英语。 原型由Jones等人描述。

3.  Disjunctive AMR

4.  AMR extensions  
    最后，我们想加深AMR语言，使其包含更多的关系。最终，我们还希望提供一整套更抽象的框架。