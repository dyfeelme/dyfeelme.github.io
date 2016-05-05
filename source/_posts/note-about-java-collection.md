---
title: java集合浅析
tags:
  - java
categories:
  - java
date: 2012-11-04 12:47:52
---

本文介绍Java基础中的集合。
<!-- more -->

## Collection接口 ##
为了方便记忆，大致画了一下类图，如下：
{% img Collection接口概览 /images/note-about-java-collection-uml.png %}

## Map接口 ##
同上，我们先画一下类图：
{% img Map接口类图 /images/note-about-java-collection-map-uml.png %}

## 用法及比较 ##
* ArrayList内部是基于数组实现的，默认扩容策略为10个大小
* Vector 被设计为线程安全的集合，初始化大小为10
* Stack 是Vector的子类，通过push(),pop()实现了后进先出(LIFO)的堆栈机制
* LinkedList 内部是一个双向链表，所以随机增删比ArrayList要快，索引比ArrayList慢
* HashMap 基于Hash算法实现的Key-Value结构,其中key和value均可以为null,存数据的时候，如果key相同，则覆盖原值。
* HashSet 内部通过HashMap来实现，value可以为null
* Hashtable 线程安全的Map实现类