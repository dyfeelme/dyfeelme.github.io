---
title: JVM内存溢出相关问题
tags:
  - stackoverflow
  - java
  - jvm
categories:
  - stackoverflow
date: 2015-07-13 12:38:16
---


## 问题 ##
平时我们遇到最多的内存溢出的问题，我这里大略总结为以下三种

 * OutOfMemoryError: Java heap space
 * OutOfMemoryError: PermGen space
 * OutOfMemoryError: unable to create new native thread

## 解决方案 ##
根据实际情况,首先应排查应用项目本身的问题,除此之外,
Java heap space的问题我们可以通过增大heap内存（即堆内存）来解决，比如
 ```bash
 -Xms:1024m -Xmx:1024m
 ```
 其中Xms指初始堆大小，默认为物理机内存的1/64，Xmx指最大堆大小,默认为物理机内存的1/4。注意：堆内存受限于操作系统。[详细](http://rabbit-saying.github.io)

 PermGen space 可以通过减少或者共享第三方jar库来解决，或者调整以下参数
 ```bash
 -XX:PermSize=64M -XX:MaxPermSize=128m
 ```

 至于最后一种无法创建本地线程的问题，需要根据实际情况进行计算：
 具体计算公式如下：
 ```code
 (MaxProcessMemory - JVMMemory - ReservedOsMemory) / (ThreadStackSize) = Number of threads
 ```

 * MaxProcessMemory	指的是一个进程的最大内存
 * JVMMemory        JVM内存
 * ReservedOsMemory 保留的操作系统内存
 * ThreadStackSize  线程栈的大小

比如，32位的windows的MaxProcessMemory为2G,eclipse默认启动JVMMemory为64M，ReservedOsMemory一般为130M左右，JDK 1.6默认的ThreadStackSize为325k,所以代入公式为（2*1024*1024-64*1024）/325=5841。
所以理论上分配给JVM的内存越大就会制约它所能创建的线程数。

## 小结 ##
解决内存溢出的问题当然不能依赖于调增JVM内存，更重要的是对项目进行质量上的监管和优化，然后配合JVM进行优化。
