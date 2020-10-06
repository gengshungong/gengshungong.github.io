# tffeb.github.io

使用
====================================

下载
------------------------------------

使用git从[tffeb.github.io](https://github.com/Tffeb/tffeb.github.io.git)主页下载项目

``` bash
git clone https://github.com/Tffeb/tffeb.github.io.git
```

配置
------------------------------------

`tffeb.github.io`项目需要配置的只有一个文件`_config.yml`，打开之后按照如下进行配置。

``` bash
name: 博客名称
email: 邮箱地址
author: 作者名
url: 个人网站
baseurl: ""
resume_site: 个人简历
github: github地址
github_username: github用户名称
# 请到百度统计官网[https://tongji.baidu.com/](https://tongji.baidu.com/)申请自己的网站ID并在此处替换，否则将无法正常统计访问量
# baidu_analysis: 49a7cfa6b548ec9bf285a5c8d1684b1f
```

如何写文章
------------------------------------

在`LessOrMore/_posts`目录下新建一个文件，可以创建文件夹并在文件夹中添加文件，方便维护。在新建文件中粘贴如下信息，并修改以下的`titile`,`date`,`categories`,`tag`的相关信息，添加`* content {:toc}`为目录相关信息，在进行正文书写前需要在目录和正文之间输入至少2行空行。然后按照正常的Markdown语法书写正文。

``` bash
---
layout: post
#标题配置
title:  标题
#时间配置
date:   2016-08-27 01:08:00 +0800
#技术栈分类配置
categories: document
#标签分类配置
tag: 标签
---

* content
{:toc}


我是正文。我是正文。我是正文。我是正文。我是正文。我是正文。
```

执行
------------------------------------

``` bash
jekyll server
```

效果
------------------------------------
打开浏览器并输入URL`http://localhost:4000/`,回车。


关于我
====================================

暂无

写在最后
====================================

暂无