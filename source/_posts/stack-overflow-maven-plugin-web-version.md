---
title: 关于升级maven构建webapp版本的问题
tags:
  - stackoverflow
  - java
  - maven
categories:
  - stackoverflow
date: 2015-04-26 10:32:30
---

使用maven构建器生成webapp项目所遇到的问题。

<!-- more -->

## 问题 ##
工作中如果我们通过maven来管理项目，由于maven的一些插件更新比较慢，比如本文所述maven-archetype-webapp,目前版本为1.0或1.1，如果我们构建器插件来新建一个webapp项目的时候，那么默认配置将会是基于jdk1.5和web2.3的项目，so 问题来了!我们要怎样将此项目变更为基于jdk1.7或web 3.0的项目呢?

## 解决方案 ##
当然你可以使用新建动态项目之流的方式，当本文所述依然为maven插件形式。

* 你可以升级上述maven-archetype-webapp插件，发布到工作组的私服中。
* 切换至项目所在目录，编辑.setting目录下的org.eclipse.wst.common.project.facet.core.xml文件，如下：

```code
<?xml version="1.0" encoding="UTF-8"?>
<faceted-project>
  <fixed facet="wst.jsdt.web"/>
  <installed facet="jst.web" version="3.0"/><!-- 此处配置web.xml的版本-->
  <installed facet="wst.jsdt.web" version="1.0"/>
  <installed facet="java" version="1.8"/><!-- 此处配置jdk的版本-->
</faceted-project>
```
当然别忘记更新项目中web.xml中的描述文件，如下可选：

web.xml 2.5
```code
<?xml version="1.0" encoding="UTF-8"?>  
<web-app xmlns="http://java.sun.com/xml/ns/javaee"  
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
    xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"  
    version="2.5">  
       
</web-app>
```

web.xml 3.0
```code
<?xml version="1.0" encoding="UTF-8"?>      
<web-app  
    version="3.0"  
    xmlns="http://java.sun.com/xml/ns/javaee"  
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
    xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd">  
       
</web-app>
```

* 配合maven-plugin-compile插件，设置编译版本为jdk1.7,如下：

```code
<plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <configuration>
          <!-- or whatever version you use -->
          <source>${java.version}</source>
          <target>${java.version}</target>
        </configuration>
</plugin>
```