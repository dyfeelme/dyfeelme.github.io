---
title: 使用AppFuse快速开始SSH项目
tags:
  - ssh
  - java
categories:
  - java
date: 2013-04-28 12:38:12
---


## 简介 ##
{% img AppFuse Logo /images/apf-logo.jpg 38 38 %}
[AppFuse](http://appfuse.org/display/APF/Home)是一款用来快速构建WEB应用的全栈框架。

## 特性 ##
AppFuse作为一个社区比较活跃的快速开发框架，主要有以下特点：
* 前端使用 Bootstrap and jQuery
* 后端使用 Maven, Hibernate, Spring and Spring Security
* 支持 Java 7, Annotations, JSP 2.1, Servlet 3.0
* 支持主流Web Frameworks: GWT, JSF, Struts 2, Spring MVC, Tapestry 5, Wicket
* JPA Support 

## 安装 ##
AppFuse需要安装jdk和maven，环境配置本文不再赘述，请参考其他文章。

## 起步 ##
有了maven和jdk环境，我们便可以开始初始化一个项目了，如下：
``` java
$ mvn archetype:generate -B -DarchetypeGroupId=org.appfuse.archetypes -DarchetypeArtifactId=appfuse-basic-spring-archetype -DarchetypeVersion=3.5.0 -DgroupId=com.dy.framework -DartifactId=appfuse-web -DarchetypeRepository=https://oss.sonatype.org/content/repositories/appfuse
```
此命令将会生成一个appfuse-web的项目。
官方提供了一个可以快速生成定制命令的页面，[详情](http://appfuse.org/display/APF/AppFuse+QuickStart)

## 配置数据库 ##
数据库的配置只需要在项目pom.xml中的_<properties>_结点内,增加以下参数：
``` xml
<hibernate.dialect>org.hibernate.dialect.MySQLDialect</hibernate.dialect>
<jdbc.groupId>mysql</jdbc.groupId>
<jdbc.artifactId>mysql-connector-java</jdbc.artifactId>
<jdbc.version>5.1.27</jdbc.version>
<jdbc.driverClassName>com.mysql.jdbc.Driver</jdbc.driverClassName>
<jdbc.url>
    <![CDATA[jdbc:mysql://localhost/${db.name}?createDatabaseIfNotExist=true&amp;useUnicode=true&amp;characterEncoding=utf-8&amp;autoReconnect=true]]>
</jdbc.url>
<jdbc.username>root</jdbc.username>
<jdbc.password/>
<jdbc.validationQuery><![CDATA[SELECT 1 + 1]]></jdbc.validationQuery>
```
上述这些参数已经在maven的父pom中指定，实际的项目需要重写这些配置。
接下来我们需要配置一下数据库：
``` bash
$ mysql -u root -p
mysql > create database db_appfuse_web default charactor set utf8;
mysql > grant all privileges on db_appfuse_web.* to admin@'%' identified by '123456';
mysql > flush privileges;
```
如上，我们建立了一个名为db_appfuse_web的数据库，并且新建并授权了名为admin的用户可以远程访问的权限。详情请参考另一篇博文[Mysql数据库笔记]。

## 启动 ##
``` bash
$ mvn jetty:run
```

## 参考 ##
[AppFuse文档](http://appfuse.org/display/APF/Reference+Guide)
