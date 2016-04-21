---
title: 关于'The submodule *** was not properly initialized with a .gitmodules file'
tags:
  - stackoverflow
  - git
categories:
  - stackoverflow
  - git
date: 2015-04-21 11:15:22
---


## 问题描述 ##

``` bash
$ Your page is having problems building: The submodule themes/next was not properly initialized with a .gitmodules file. For more information, see https://help.github.com/articles/page-build-failed-missing-submodule.
```

## 分析 ##

此问题一般是因为git仓库中引用其他git仓库，而未通过子模块添加或初始化原因导致的。

## 解决方案 ##

在已经通过git版本控制的代码库里，如果需要引入另外一个git管理的项目时，我们可以通过 *git submodule*命令来添加

```bash
$ git submodule add https://github.com/xxx.git /path/xxx
```

## 参考 ##
* [GIT 子模块](https://git-scm.com/book/zh/v1/Git-%E5%B7%A5%E5%85%B7-%E5%AD%90%E6%A8%A1%E5%9D%97)

