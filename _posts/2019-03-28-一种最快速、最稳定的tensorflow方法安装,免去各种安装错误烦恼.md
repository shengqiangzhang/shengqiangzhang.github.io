---
layout:     post
title:      一种最快速、最稳定的tensorflow方法安装,免去各种安装错误烦恼
subtitle:   跳过一些常见的坑
date:       2019-03-28
author:     Shengqiang Zhang
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - python
---

##  一些常见的坑

今天在python3.7环境下安装tensorflow出现了各种意外，最终还是解决了。首先是tensorflow与cuda版本之间不匹配，tensorflow1.0版本以上是不支持cuda8.0以下的。接着又是tensorflow与python版本不匹配，目前python3.7虽然能够使用tensorflow，但是需要一些修改，而使用python3.6就可以轻易安装了。

通过今天遇到的坑，总结出一种快速无误安装tensorflow的方式，通过使用Anaconda自动匹配安装tensorflow及其依赖的文件。

## 安装Anaconda

首先，通过[Anaconda][1]下载符合你系统的命令行安装包或者图形安装包。`Graphical Installer`表示图形安装包，一步一步安装提示安装即可。`Command Line Installer`表示命令行安装包，具体安装方式如下：
```python
# 执行安装
./Anaconda3-2018.12-MacOSX-x86_64.sh

# 若出现permission denied，则表示权限不足
# 执行下列命令
sudo chmod -R 777 当前文件所在的文件夹名称
```

安装过程中，根据提示操作，一般情况下出现提示只需要按Enter或者输入yes或者输入y即可。安装过程请耐心等待。

## 安装python3.6及tensorflow

请先关闭终端后，再重新打开终端，以便使得Anaconda的安装生效。

```python
# 创建一个python3.6环境
# 前面表示环境名称python36，后面表示python的版本
# 安装过程有任何提示请输入yes或者y
conda create -n python36 python=3.6

# 激活环境
source activate python36

# 开始安装tensorflow
# windows和Linux系统可自由选择安装tensorflow和tensorflow-gpu
# macOSX由于闭源，所以建议安装tensorflow版本，tensorflow-gpu的安装方式请自行查看其他教程
pip install tensorflow


# 退出环境
source deactivate

#查看已有环境
conda info -e
```

以后每次进入python3.6环境的时候，只需要执行`source activate python36`就可以了。


[1]:https://www.anaconda.com/distribution/#macos