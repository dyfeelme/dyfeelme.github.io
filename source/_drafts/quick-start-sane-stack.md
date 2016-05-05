---
title: JavaScript全栈开发框架-SANE
tags:
---
[SANE](http://sanestack.com/)是一款使用Sails和Ember编写的可用于生产准备的JavaScript全栈开发框架。
<!-- more -->

## 快速开始 ##

``` bash
$ npm install -g sails sane-cli

生成初始项目
$ sane new project --docker

生成一个后端的API和前端的model
$ sane generate resource user name:string age:number

启动服务
$ sand up

```

## 命令概览 ##
``` bash
新建项目
sane new project [--docker] [-d mongo|postgres|mysql|disk] [--verbose] [--skip-npm] [--skip-bower]
启动服务
sane up [--docker], alias: sane serve
生成API和资源
sane generate api|resource <name> [--pod] [attribute1:type1, attribute2:type2 ... ], alias: sane g

```

## 配置 ##
.sane-cli

* apps: array
	‘client’ => Expected folder-name: client 
	‘clientv1’ => Expected folder-name: clientv1 
	‘admin-v1-client’ => Expected folder-name: admin-v1 
	‘server’ => Expected folder-name: server 
	‘server2’ => Expected folder-name: server2 
	‘api-v1-server’ => Expected folder-name: api-v1 
* disableAnalytics: true|false Used to disable the anonymous analytics. database: postgres|mysql|mongo Currently not in use. 
* docker: true|false Runs all commands via compose 
* verbose: true|false Shows extra output on some commands 
* skipNpm: true|false Only used if defined in your home-directory 
* skipBower: true|false Only used if defined in your home-directory

例如：
``` bash
.sane-cli
{
  "apps": [
    "client",
    "server"
  ],
  "disableAnalytics": false,
  "database": "postgresql",
  "docker": false,
  "verbose": false,
  "skipNpm": true,
  "skipBower": true
}
```

