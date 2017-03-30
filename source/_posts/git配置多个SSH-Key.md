---
title: git配置多个SSH-Key
date: 2017-02-08 17:02:23
tags: 工具
categories: 工具
---

## 具体操作步骤

#### 1、生成一个公司用的SSH-Key

``` bash
$ ssh-keygen -t rsa -C "youremail@yourcompany.com" -f ~/.ssh/id_rsa
```

在~/.ssh/目录会生成id_rsa和id_rsa.pub私钥和公钥。 我们将id-rsa.pub中的内容粘帖到公司gitlab服务器的SSH-key的配置中

#### 2、生成一个github用的SSH-Key

``` bash
$ ssh-keygen -t rsa -C "youremail@your.com" -f ~/.ssh/github_rsa
```

在~/.ssh/目录会生成github_rsa和github_rsa.pub私钥和公钥。 我们将github_rsa.pub中的内容粘帖到github服务器的SSH-key的配置中
<!--more-->
#### 3、添加私钥
```bash
$ ssh-add ~/.ssh/id_rsa $ ssh-add ~/.ssh/github_rsa
```
如果执行ssh-add时提示"Could not open a connection to your authentication agent"，可以现执行命令：
```bash
$ ssh-agent bash
```
然后再运行ssh-add命令
```bash
# 可以通过 ssh-add -l 来确私钥列表
$ ssh-add -l
# 可以通过 ssh-add -D 来清空私钥列表
$ ssh-add -D
```
#### 4、修改配置文件
在 ~/.ssh 目录下新建一个config文件
```bash
touch config
```
添加内容
```bash
# gitlab
Host gitlab.com
    HostName gitlab.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa
# github
Host github.com
    HostName github.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/github_rsa
```
#### 6、测试
```bash
$ ssh -T git@github.com
```
输出
Hi stefzhlg! You've successfully authenticated, but GitHub does not provide shell access.

就表示成功的连上github了.也可以试试链接公司的gitlab

More info: [Deployment](https://hexo.io/docs/deployment.html)
