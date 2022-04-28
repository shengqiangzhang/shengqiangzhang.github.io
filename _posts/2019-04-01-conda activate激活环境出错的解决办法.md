---
layout:     post
title:      conda activate激活环境出错的解决办法
subtitle:   Anaconda conda activate激活环境出错的解决办法
date:       2019-04-01
author:     Shengqiang Zhang
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - python
---

# 出现错误情况
今天在实用Anaconda激活python3.6环境的时候出现了如下错误：
```python
[zsq@localhost ~]$ conda activate python36

CommandNotFoundError: Your shell has not been properly configured to use 'conda activate'.
To initialize your shell, run

    $ conda init <SHELL_NAME>

Currently supported shells are:
  - bash
  - fish
  - tcsh
  - xonsh
  - zsh
  - powershell

See 'conda init --help' for more information and options.

IMPORTANT: You may need to close and restart your shell after running 'conda init'.
```
google一番发现了几个解决办法，但是还是没能成功解决。后面仔细想想，发现是上次进入该服务器实用`conda activate python36`激活环境后未使用`conda deactivate`退出环境就关闭终端导致的。

发现这个问题后，解决思路就比较明显了，重新激活一下环境就好了，具体操作如下：
```python
# 重新进入虚拟环境
source activate
# 重新退出虚拟环境
```

最后，重新执行`conda activate python36`，没有报错，成功进入该虚拟环境。
