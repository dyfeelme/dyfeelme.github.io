---
title: 高性能in-memory分布式平台-Hazelcast
tags:
  - 分布式
categoriest:
 - java
date: 2016-04-28 11:06:48
---


## 简介 ##
{% blockquote Hazelcast https://github.com/hazelcast/hazelcast Github-Hazelcast%}
Hazelcast is a clustering and highly scalable data distribution platform.
{% endblockquote %}

Hazelcast 提供了分布式数据结构处理和其他In-Memory计算，最简单的，它可以很容易的实现java并发包的ConcurrentHashMap来支持JVM的多线程访问操作，但Haze了cast要做的绝不止这样，以下为Hazelcast的宏伟蓝图：
{% img [hazelcast architecture] /images/hazelcast-architecture-20160428.png 450 400 Hazelcast架构图 %}
所以Hazelcast支持众多不同平台体系，并提供了企业定制的高级功能。

## 特性 ##
Hazelcast是Java编写的开源实现，支持Java6\7\8 SE，并提供弹性，冗余和高性能的特性。

## 快速开始 ##
Hazelcast保持了单一引用的jar包，所以很容易上手，如下：
``` java
引入Maven依赖：
<dependency>
    <groupId>com.hazelcast</groupId>
    <artifactId>hazelcast</artifactId>
    <version>${hazelcast.version}</version>
</dependency>
简单实现多线程可并发的HashMap:

Map<String, Customer> mapCustomers = Hazelcast.getMap("customers");
mapCustomers.put("1", new Customer("Joe", "Smith"));
mapCustomers.put("2", new Customer("Ali", "Selam"));
mapCustomers.put("3", new Customer("Avi", "Noyan"));
 
Collection<Customer> colCustomers = mapCustomers.values();
for (Customer customer : colCustomers) {
    // process customer
}
```

## 参考 ##
[Hazelcast官方文档](http://hazelcast.org/deployment-operations-guide/)

