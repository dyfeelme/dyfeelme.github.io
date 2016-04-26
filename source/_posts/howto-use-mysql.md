---
title: Mysql数据库笔记
tags:
  - howto
  - database
  - mysql
categories:
  - howto
  - database
date: 2016-04-26 19:53:48
---


## 概述 ##

## 安装 ##

```code
ubuntu
$ sudo apt-get update && sudo apt-get install mysql-server-5.6

centos
$ sudo yum install mariadb-server
```

## 配置 ##

```bash
$ /etc/mysql/my.ini
为了能进行远程登录，注释掉bing-address=127.0.0.1一行
```

## 操作 ##

* 登录

```bash
$ mysql -u root -h localhost -p
```

* 建库

```bash
$ create database db_name default character set utf8;
```

* 授权

```bash
$ grant all privileges on db_name.* to user@'%' identified by 'password';
上述命令授权的同时新建了用户，如要授权已有用户，则不需要指定 identified by 'password'
其中%代表所有IP，即可以进行远程登陆。
$ flush privilges;
```

* 建表

```bash
$ create table t_tablename (
    ID BIGINT NOT NULL,
    NAME  VARCHAR(200) NOT NULL,
    DESCRIPTION VARCHAR(250) NULL,
    DATA BLOB NULL,
    PRIMARY KEY (ID));
```

* 删除表

```bash
$ drop table if exists t_tablename;
```

* 删除数据库

```bash
$ drop database if exists db_name;
```

* 导入脚本

```bash
$ mysql -u user -h localhost -p password -D db_name < /path/script.sql
或者
mysql> source /path/script.sql
或者
mysql> \. /path/script.sql
```