---
title: NodeJS入门-sails
tags:
  - nodejs
  - javascirpt
categories:
  - NodeJS
date: 2016-02-05 17:14:32
---


{% img sails /images/sails-logo.png %}
[sails](http://sailsjs.org/)是一款类似于Java,Ruby等可以提供REST, HTTP, WebSockets等协议或接口的后端nodejs框架。
<!-- more -->

## 快速开始 ##
``` bash
$ npm install -g sails	# 安装
$ sails new sails-web	# 创建web项目
$ sails lift			# 启动服务
```

## 命令概览 ##
``` bash
  Usage: sails [command]

  Commands:
    version                        
    lift|l [options]               
    new [options] [path_to_new_app]
    generate                       
    deploy                         
    console|c                      
    www                            
    debug                          
    help                           
    *                              

  Options:
    -h, --help     output usage information
    -v, --version  output the version number
    --silent       
    --verbose      
    --silly        

```

## 创建REST API ##
``` bash
$ sails generate api user
```
上述命令生成了User的model和controller,如下：
api/models/User.js
``` javascript
/**
 * User.js
 *
 * @description :: TODO: You might write a short summary of how this model works and what it represents here.
 * @docs        :: http://sailsjs.org/documentation/concepts/models-and-orm/models
 */

module.exports = {

  attributes: {

  }
};
```
api/controllers/UserController.js
``` javascript
/**
 * UserController
 *
 * @description :: Server-side logic for managing users
 * @help        :: See http://sailsjs.org/#!/documentation/concepts/Controllers
 */

module.exports = {
	
};
```
