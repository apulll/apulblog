---
title: Hexo 源码存放
date: 2017-03-30 14:36:35
tags: 工具
categories: 工具
---
 ### 对于github 博客和源码存放问题求解

1. username.github.io 域名下对应着开发者 在github 上的一个项目文件（存放着生成后的文件），现在我们需要存放源码在远程，在github上再新建一个repository.
2. 本地项目更新到远程目录，中间会遇到一个问题（`fatal: refusing to merge unrelated histories`）,解决方法 `git pull origin master --allow-unrelated-histories` .
3. 至此本地源码也保存到了远程