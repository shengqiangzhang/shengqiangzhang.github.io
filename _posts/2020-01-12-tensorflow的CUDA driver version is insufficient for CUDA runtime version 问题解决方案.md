--- 
layout: article
title: tensorflow的CUDA driver version is insufficient for CUDA runtime version 问题解决方案
---

CUDA driver version is insufficient for CUDA runtime version 翻译过来就是CUDA的驱动程序版本跟CUDA的运行时版本不匹配

## 1.查看CUDA driver version \(驱动版本\):

```bash
nvidia-smi
```

<!--more-->

![](http://39.106.118.77/wp-content/uploads/2020/01/b43554f41df5d23ea2df6660c8cce42b.png)

显示的驱动程序版本是：384.145

## 2.查看CUDA runtime version \(运行时版本\):

```bash
conda list cudatoolkit
conda list cudnn
```

![](http://39.106.118.77/wp-content/uploads/2020/01/3f57b0e3dc49a764991b40f70e691123.png)

python安装的cudatoolkit和cudnn程序包版本是：9.0

## 3.nvidia 驱动和cuda runtime 版本对应关系

| 运行时版本 | 驱动版本 |
| --- | --- |
| CUDA 9.1   |   387.xx |
| CUDA 9.0   |   384.xx |
| CUDA 8.0   |   375.xx \(GA2\) |
| CUDA 8.0   |   367.4x |
| CUDA 7.5   |   352.xx |
| CUDA 7.0   |   346.xx |
| CUDA 6.5   |   340.xx |
| CUDA 6.0   |   331.xx |
| CUDA 5.5   |   319.xx |
| CUDA 5.0   |   304.xx |
| CUDA 4.2   |   295.41 |
| CUDA 4.1   |   285.05.33 |
| CUDA 4.0   |   270.41.19 |
| CUDA 3.2   |   260.19.26 |
| CUDA 3.1   |   256.40 |
| CUDA 3.0   |   195.36.15 |

## 4.解决方案

从驱动和运行时的版本对应关系来看，版本为384.xx的驱动程序 对应的 运行时版本是9.0，也就是说我们在python中安装cudatoolkit和cudnn程序包版本应该是9.0，如果显示的是9.2的话，需要重新安装。

```bash
conda uninstall cudnn cudatoolkit

# cudatoolkit安装对应版本号
conda install cudatoolkit=9.0
conda install cudnn

# 重新安装tensorflow-gpu
conda install tensorflow-gpu=1.13

```

 

5.为什么会出现这种情况呢：

一般出现这种情况是因为在python中安装tensorflow的gpu版本时，pip会检查tensorflow依赖的其他的包，如果依赖的包没有安装，则会先安装最新版本的依赖包。这时候tensorflow的gpu版本依赖cudatoolkit和cudnn程序包，pip就会安装最新版本的cudatoolkit和cudnn程序包，最终导致gpu驱动版本和cuda运行时版本不匹配。