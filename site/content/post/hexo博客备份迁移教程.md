---
title: hexo博客备份迁移教程
comments: true
toc: true
categories:
  - hexo
tags:
  - hexo
  - hexo备份还原
abbrlink: 3
slug: 3
date: 2019-09-11 13:01:13
---

# hexo备份
## 新建repository
在Github下创建一个新的repository，取名为myblog。(与本地的Hexo源码文件夹同名即可)
创建的时候最好为空，不要勾选创建README.md。
<!-- more -->
## 创建仓库
进入本地的Hexo文件夹(D:\hexo\blog\myblog)，在这个地方使用git Bash here执行以下命令创建仓库
## 创建.gitignore文件

```
touch .gitignore
```
参考我的 .gitignore：（下面的文件不备份）
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
## 提交Hexo源码
git add .
git commit -m "添加hexo源码文件作为备份"

## 删除远程库
git remote rm origin
## 添加远程 Git 仓库
git remote add origin git@github.com:waimao8/myblog.git
## 远程仓库合并到本地
git pull --rebase origin master

## 更新远程仓库
git push -u origin master
# hexo备份还原
在任何一台电脑上，只需要git remote add origin git@github.com:waimao8/myblog.git,即可完成将Hexo源文件复制到本地

在本地编写完博客时，顺次执行实现三步骤，即可完成Hexo博客源文件更新同步

## 提交Hexo源码
git add .
git commit -m "添加hexo源码文件作为备份"
## 远程仓库合并到本地
git pull --rebase origin master
## 更新远程仓库
git push -u origin master
