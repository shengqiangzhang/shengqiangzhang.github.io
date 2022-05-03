---
layout: post
title: 为Jupyter Notebook配置多个python版本
---

在实用Anaconda过程中，默认为安装python2或者python3，而使用jupyter notebook时，默认只有一个python版本，为了能够方便随时切换python版本，可以为jupyter notebook安装多个python内核。

## 1. 只存在python2虚拟环境：

```bash
conda create -n ipykernel_py3 python=3.6 ipykernel
source activate ipykernel_py3 # mac
activate ipykernel_py3 # windows
python -m ipykernel install --user
```

## 2. 只存在python3虚拟环境

```bash
conda create -n ipykernel_py2 python=2.7 ipykernel
source activate ipykernel_py2 # mac
activate ipykernel_py2 # windows
python -m ipykernel install --user
```

## 3. 已经存在python2和python3虚拟环境

```bash
source activate 你的虚拟环境名称 # mac
activate 你的虚拟环境名称 # windows
python -m ipykernel install --user
```