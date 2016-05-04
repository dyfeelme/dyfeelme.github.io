---
title: Java多线程编程-高级锁
tags:
  - java
categories:
  - java
date: 2015-11-14 12:47:28
---


## Lock 接口##
多线程里，如果一个资源是共享的，为了保证数据的完整和一致性，我们通常需要在事务操作时对资源进行加“锁”，这样就能保证在事务操作时只能有一个线程进行操作，传统情况我们通过Java提供的Synchronized 对代码块儿进行加锁
{% img Lock接口概览图 /images/note-about-java-lock.png  %}
{% img Lock接口概览图 /images/note-about-java-lock-impl.png %}
