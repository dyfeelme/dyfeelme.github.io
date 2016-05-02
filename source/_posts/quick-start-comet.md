---
title: 基于长轮询的解决方案－comet
tags:
  - java
  - comet
categoriest:
  - java
date: 2015-05-01 15:33:24
---


## 概述 ##
{% blockquote Wiki https://en.wikipedia.org/wiki/Comet_(programming) Wiki-Comet %}
Comet是一种用于web的推送技术，能使服务器实时地将更新的信息传送到客户端，而无须客户端发出请求，目前有两种实现方式，长轮询和iframe流。
{% endblockquote %}

## iframe ##
iframe流方式是在页面中插入一个隐藏的iframe，利用其src属性在服务器和客户端之间创建一条长链接，服务器向iframe传输数据（通常是HTML，内有负责插入信息的javascript），来实时更新页面。

iframe流方式的优点是浏览器兼容好，Google公司在一些产品中使用了iframe流，如Google Talk。

## 长轮询 ##
长轮询是在打开一条连接以后保持，等待服务器推送来数据再关闭的方式。


## 参考 ##

[Wiki-Comet](https://en.wikipedia.org/wiki/Comet_(programming))