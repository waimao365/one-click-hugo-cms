---
title: hexo博客优化之文章置顶+置顶标签
comments: true
toc: true
categories:
  - hexo
tags:
  - hexo
  - 网站

abbrlink: 4
slug: 4
date: 2019-09-12 13:01:23
---
[支持置顶的仓库](https://github.com/netcan/hexo-generator-index-pin-top)

可以直接用以下命令安装

```
$ npm uninstall hexo-generator-index --save
$ npm install hexo-generator-index-pin-top --save
```
然后在需要置顶的文章的Front-matter中加上top: true即可。
<!-- more -->
**设置置顶标志**

打开：/blog/themes/next/layout/_macro 目录下的post.swig文件，定位到

```
<div class="post-meta">
```
下面插入如下代码：

```
{% if post.top %}
            <i class="fa fa-thumb-tack"></i>
            <font color=7D26CD>置顶</font>
            <span class="post-meta-divider">|</span>
          {% endif %}

```



