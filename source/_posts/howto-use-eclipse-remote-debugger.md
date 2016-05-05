---
title: 使用Eclipse对应用进行远端调试
tags:
  - eclipse
  - debug
  - jpda
categories:
  - java
date: 2014-08-13 14:58:20
---
{% blockquote IBM DeveloperWorks %}
JPDA（Java Platform Debugger Architecture）是 Java 平台调试体系结构的缩写，通过 JPDA 提供的 API，开发人员可以方便灵活的搭建 Java 调试应用程序。 JPDA 主要由三个部分组成：Java 虚拟机工具接口（JVMTI），Java 调试线协议（JDWP），以及 Java 调试接口（JDI）。
{% endblockquote %}
<!-- more -->

## 实践 ##

开启远程调试端口
```bash
-Xdebug -Xrunjdwp:transport=dt_socket, address=8000,server=y,suspend=y
```

* -Xdebug 启用调试特性
* -Xrunjdwp 启用JDWP实现，它包含若干子选项：
 transport=dt_socket JPDA front-end和back-end之间的传输方法。dt_socket表示使用套接字传输。
 address=8000 JVM在8000端口上监听请求。
 server=y y表示启动的JVM是被调试者。如果为n，则表示启动的JVM是调试器。
 suspend=y y表示启动的JVM会暂停等待，直到调试器连接上。

suspend=y这个选项很重要。如果你想从Tomcat启动的一开始就进行调试，那么就必须设置suspend=y。

本地maven调试
将以上参数添加至maven启动参数，或者配置到MAVEN_OPTS环境变量中

服务器tomcat调试
将以上参数添加至tomcat启动参数中

配置Eclipse调试器
打开eclipse -> run -> run config，如图：
{% img Eclipse运行配置窗口 http://www.ibm.com/developerworks/cn/opensource/os-eclipse-javadebug/debugconfig.jpg 500 500 %}

## 参考 ##
[维基百科](https://en.wikipedia.org/wiki/Java_Platform_Debugger_Architecture)
[IBM DeveloperWorks](http://www.ibm.com/developerworks/cn/java/j-lo-jpda1/index.html)
