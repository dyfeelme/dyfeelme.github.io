---
title: Linux命令小记-SCP
tags:
  - note
  - linux
  - shell
categories:
  - 操作系统
  - linux
date: 2016-01-26 19:24:28
---


## 概述 ##
SCP（Secure Copy）远程安全拷贝，是一个不需要通过FTP,WEB等额外服务就可以完成终端之间文件传输的命令行工具。

## 命令 ##
* 获取远程服务器上的文件

``` bash
$ scp -P 2222 username@ip:/path/filename local_filename
```

* 获取远程服务器上的目录

``` bash
$ scp -P 2222 -r username@ip:/path/ local_dir
```

* 将本地文件传输至服务器指定目录

``` bash
$ scp -P 2222 local_file username@ip:/path/filename
```

* 将本地目录传输至服务器指定目录

``` bash
$ scp -P 2222 -r local_dir username@ip:/path/
```

## 参数 ##

``` bash
-v 用来显示进度，查看连接，认证，或是配置错误。

-C 使能压缩选项。

-4 强行使用 IPV4 地址。

-6 强行使用 IPV6 地址。
```

