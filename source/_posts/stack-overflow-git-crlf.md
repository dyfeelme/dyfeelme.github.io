---
title: 'Git CRLF问题'
tags:
  - stackoverflow
  - git
categories:
  - stackoverflow
  - git
date: 2016-04-13 11:00:25
---


## 问题描述 ##
```bash
warning: LF will be replaced by CRLF in ***
```
## 解决方法 ##

windows:
```bash
D:\dev git config --global core.autocrlf true
```

macos:
```bash
$git config --global core.autocrlf input
```
