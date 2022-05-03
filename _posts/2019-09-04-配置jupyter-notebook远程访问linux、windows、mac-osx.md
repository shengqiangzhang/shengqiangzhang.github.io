---
layout: article
title: 配置Jupyter Notebook远程访问(Linux、Windows、mac OSX通用)
---

1.  执行以下命令:
    ```bash
    jupyter notebook --generate-config
    ```

    此时会在**当前用户目录**的`.jupyter`目录下会生成一个`jupyter_notebook_config.py`的配置文件

<!--more-->

2.  执行以下命令:

    ```bash
    python -c "import IPython;print(IPython.lib.passwd())"
    ```

    生成一个hash密码，_并记下来_

3.  编辑配置文件, Linux或Mac OSX系统可执行以下命令来编辑配置文件

    ```bash
    vim ~/.jupyter/jupyter_notebook_config.py
    ```

    windows用户请跳转到目录`C:\Users\USERNAME\.jupyter`中查找并编辑配置文件`jupyter_notebook_config.py`

    并在末尾追加以下配置内容:

    ```bash
    c.NotebookApp.password = u'sha1:刚刚生成的hash密码'
    c.NotebookApp.ip = '*' # *表示任何人都可以访问
    c.NotebookApp.port = 13823 # 端口号
    c.NotebookApp.open_browser = False # 一般是通过ssh远程连接, 设置为不自动打开浏览器
    ```

4.  执行以下命令:
    ```bash
    jupyter notebook
    ```

    启动jupyter notebook，并在远程计算机中通过**服务器ip:port**的形式进行远程访问。

    此时，若关闭终端，则jupyter notebook会自动关闭，为了能够使得jupyter notebook在后台运行，可执行以下命令:

    ```bash
    nohup jupyter notebook > output_file.out 2>&1 &
    exit
    ```