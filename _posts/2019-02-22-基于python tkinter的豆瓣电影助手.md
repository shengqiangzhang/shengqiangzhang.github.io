---
layout:     post
title:      基于python tkinter的豆瓣电影助手
subtitle:   python tkinter学习笔记
date:       2019-02-22
author:     Shengqiang Zhang
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - python
    - tkinter
    - 爬虫
---



# 项目简介

这个项目源于大三某课程设计。平常经常需要搜索一些电影，为了方便使用，就将原来的项目重新改写了。由于是基于python tkinter进行桌面端开发的，所以相对WEB端来说，可能不是特别方便。



# 配置说明

1. 打开http://phantomjs.org/download.html，根据自己的操作系统下载对应的phantomjs
2. 打开当前面目录下的**<u>getMovieInRankingList.py</u>**，定位到第86行，将`executable_path=phantomjs-2.1.1-macosx/bin/phantomjs`修改成你自己的路径，如`executable_path=xxx/bin/phantomjs`
3. 打开pycharm，依次安装以下包

- pip install Pillow
- pip install selenium==2.48.0



# 功能截图

![](https://raw.githubusercontent.com/shengqiangzhang/doubanMovieTool/master/example_rating.png)



![](https://raw.githubusercontent.com/shengqiangzhang/doubanMovieTool/master/example_keyword.png)



# 包含功能

- [x] 根据关键字搜索电影
- [x] 根据排行榜(TOP250)搜索电影
- [x] 显示IMDB评分及其他基本信息
- [x] 提供多个在线视频站点，无需vip
- [x] 提供多个云盘站点搜索该视频，以便保存到云盘
- [x] 提供多个站点下载该视频
- [ ] 等待更新



# 相关技术

- Python tkinter模块 GUI可视化
- Python基本爬虫方式
- Python正则提取数据
- selenium模拟浏览器行为



# 存在问题

目前没有加入反爬虫策略，如果运行出现403 forbidden提示，则说明暂时被禁止，解决方式如下：

- 加入cookies
- 采用随机延时方式
- 采用IP代理池方式(较不稳定)



# 补充

点击这里打开[GitHub项目地址](https://github.com/shengqiangzhang/doubanMovieTool)
