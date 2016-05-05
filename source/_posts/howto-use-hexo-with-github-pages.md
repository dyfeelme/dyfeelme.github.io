---
title: 使用Hexo打造个人博客
date: 2016-02-16 23:58:36
tags:
 - hexo
 - github
 - blog
categories:
 - 兔言兔语
---

{% img hexo https://hexo.io/logo.svg 50 50 %}
hexo 是一款基于nodejs搭建轻博客的快速构建器，支持多种风格、插件，一键部署等功能。
<!-- more -->

## 初始化 ##
```bash
$ npm install hexo-cli -g
```

## 基本命令 ##
```bash
清理数据文件
$ hexo clean
生成静态文件
$ hexo generate 或者 hexo g
启动本地服务
$ hexo server 或者 hexo s
部署
$ hexo deploy 或者 hexo d
```

## 使用主题 ##
选择一款自己喜欢的[主题](https://hexo.io/themes/),将主题文件添加至themes目录，通过配置*_config.yml*来启用新主题，注意：如果博客已经通过git管理，则需要通过以下命令将主题仓库包含至本仓库，如下：
```bash
$ git submodule add [主题仓库] themes/主题名
```
## 部署 ##
1. 安装部署插件
```bash
$ npm install hexo-deployer-git --save
```
2. 配置
编辑 *_config.yml*,github pages配置如下：
```bash
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repository: git@github.com:dyfeelme/dyfeelme.github.io.git
  branch: master
```
3. 部署到Githup Pages
仓库规划
因为我们需要将博客直接通过username.github.io作为域名发布，根据官方[文档](https://help.github.com/articles/user-organization-and-project-pages/),需要将源代码另存分支，部署文件提交至master分支上。如下操作：
```bash
创建Github SSH 私钥
$ cd ~/.ssh && ssh-keygen -t rsa -C "dyfeelme@gmail.com"
$ cat ~/.ssh/id_rsa.pub
将id_rsa.put中内容拷贝，并在github账号管理中"SSH and GPG keys"菜单中新增信任项。
新建gh-pages分支，将原代码提交至此分支
通过上文配置的部署插件，运行：
$ hexo d
命令将自动将部署文件发布至master分支，注意：会覆盖原先提交至masters上的所有代码。
```

