---
title: hexo安装后的使用教程
date: 2019-09-09 14:37:42
comments: true
toc: true
categories:
  - hexo
  - 网站
  - 博客
tags:
  - hexo
  - 网站
  - 博客

abbrlink: 1
slug: 1
---

​    

  # 安装主题（next）

git clone https://github.com/theme-next/hexo-theme-next themes/next

 下载主题解压后放到themes目录  
 编辑主目录的_config.yml 查找language 设置 language: zh-CN  
<!-- more -->
 
 搜索Schemes
 切换到 scheme: Gemini
 搜索menu找到如下配置项，将about、tags、categories前的#号去掉

更新hexo或者主题可以复制 备份好的source  文件夹替换，新安装的博客可以按照下面教程重新安装
 
 # 添加分类 


 1、创建“分类”选项  
 1.1 生成“分类”页并添加tpye属性  
 打开命令行，进入博客所在文件夹。执行命令


```
hexo new page categories

```
 成功后会提示：


```
INFO  Created: ~/Documents/blog/source/categories/index.md

```
 根据上面的路径，找到index.md这个文件，打开后默认内容是这样的：


```
---
title: 文章分类
date: 2019-04-07 0:30:00
---

```
 添加type: "categories"到内容中，添加后是这样的：


```
---
title: 文章分类
date: 2019-04-07 0:30:00
type: "categories"
---

```
 保存并关闭文件。

 
 # 给文章添加“categories”属性


 打开需要添加分类的文章，为其添加categories属性。下方的categories: web前端表示添加这篇文章到“web前端”这个分类。注意：hexo一篇文章只能属于一个分类，也就是说如果在“- web前端”下方添加“-xxx”，hexo不会产生两个分类，而是把分类嵌套（即该文章属于 “- web前端”下的 “-xxx ”分类）。


```
---
title: jQuery对表单的操作及更多应用
date: 2019-04-07 0:31:22
categories: 
- web前端
---

```
 至此，成功给文章添加分类，点击首页的“分类”可以看到该分类下的所有文章。当然，只有添加了categories: xxx的文章才会被收录到首页的“分类”中。  

# 创建“标签”选项  

 生成“标签”页并添加tpye属性  
 打开命令行，进入博客所在文件夹。执行命令


```
hexo new page tags

```
 找到 source/tags/index.md  
 添加type: "tags"到内容中，添加后是这样的


```
---
title: 文章分类
date: 2019-04-07 0:33:55
type: "tags"
---

```
 保存并关闭文件。  

 # 给文章添加标签和分类




```
title: title #文章標題
date: 2019-04-07 00:43:12 #文章生成時間
categories: "Hexo教程" #文章分類目錄 可以省略
tags: #文章標籤 可以省略
     - 标签1
     - 标签2
 description: #你對本頁的描述 可以省略

```
 # 添加菜单 


 编辑主题的_config.yml，查找menu，去掉 tags categories about 前面的#号就可以了  

 # 显示摘要 阅读全文
在文章下面添加，建议在3到5行处添加
  < !--more-->

   
# 添加版权
搜索 creative_commons
sidebar: false 改成  sidebar: true
post: false 改成 post: true

# 文章Url固定链接（修改博客根目录的_config.yml）
查找 permalink: :year/:month/:day/:title/
替换成
permalink: archives/:abbrlink.html
写文章加上 abbrlink: 1（数字越大的，就是越新的文章）

# 置顶

[支持置顶的仓库](https://github.com/netcan/hexo-generator-index-pin-top)

可以直接用以下命令安装

$ npm uninstall hexo-generator-index --save
$ npm install hexo-generator-index-pin-top --save
然后在需要置顶的文章的Front-matter中加上top: true即可。

设置置顶标志
打开：/blog/themes/next/layout/_macro 目录下的post.swig文件
查找
``` 
 <div class="post-meta">  
```
下面添加

```    
           {% if post.top %}
            <i class="fa fa-thumb-tack"></i>
            <font color=7D26CD>置顶</font>
            <span class="post-meta-divider">|</span>
           {% endif %}

```


需要置顶文章需要添加    top: true

#  添加不蒜子访问统计
 是否开启访问量统计功能(不蒜子)
busuanzi:
 enable: true
 修改next主题的模板文件
需要修改的模板文件是theme/next/layout/_partials/footer.swig
在最后面添加


``` 
{% if theme.footer.counter %}
    <script async src="//dn-lbstatics.qbox.me/busuanzi/2.3/busuanzi.pure.mini.js"></script>

    <span id="busuanzi_container_site_pv">总访问量<span id="busuanzi_value_site_pv"></span>次</span>
    <span class="post-meta-divider">|</span>
    <span id="busuanzi_container_site_uv">总访客<span id="busuanzi_value_site_uv"></span>人</span>
    <span class="post-meta-divider">|</span>

{% endif %}

```
# 添加评论
Github大礼包：gitment， gitalk（推荐），gitter（推荐）; 三个都支持Markdown；基于leancloud的无后端评论系统：Valine（推荐，支持Markdown）
本站使用
Valine+Leancloud 国际版 https://console.leancloud.app
在存储->结构化数据创建一个class并命名为comment。
在设置->应用Keys可以看到自动生成的AppID和AppKey,填到下面对应的位置就可以了

```
valine:
  enable: ture
  appid: xxxxxxx
  appkey: xxxxxx

```

# 添加阅读人数（真实人数）
id和key 也可以用上面Leancloud 国际版 的AppID和AppKey,
``` 
leancloud_visitors:
  enable: true
  app_id: xxxxx
  app_key: xxxxxx

```
# 添加阅读人数之不蒜子（虚高人数）
打开不蒜子
``` 
busuanzi_count:
  enable: ture
  
```
打开 next\layout\_partials  找到footer.swig文件，在最下面添加

``` 

{% if theme.footer.counter %}
    <script async src="//dn-lbstatics.qbox.me/busuanzi/2.3/busuanzi.pure.mini.js"></script>

    <span id="busuanzi_container_site_pv">总访问量<span id="busuanzi_value_site_pv"></span>次</span>
    <span class="post-meta-divider">|</span>
    <span id="busuanzi_container_site_uv">总访客<span id="busuanzi_value_site_uv"></span>人</span>
    <span class="post-meta-divider">|</span>

{% endif %}


```
