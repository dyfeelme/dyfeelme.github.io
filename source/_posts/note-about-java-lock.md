---
title: Java多线程编程-高级锁
tags:
  - java
categories:
  - java
date: 2015-11-14 12:47:28
---

多线程里，如果一个资源是共享的，为了保证数据的完整和一致性，我们通常需要在事务操作时对资源进行加“锁”，这样就能保证在事务操作时只能有一个线程进行操作，传统情况我们通过Java提供的synchronized关键字来实现同步，JDK1.5以后提供了java.util.concurrent.lock包，进一步提供了灵活高级的同步方式。
<!-- more -->

## 锁 ##
Java中锁的分类大致有以下几种：

* 自旋锁
自旋锁是采用让当前线程不停地的在循环体内执行实现的，当循环的条件被其他线程改变时 才能进入临界区。

``` java
public class SpinLock {
  private AtomicReference<Thread> sign =new AtomicReference<>();
  public void lock(){
    Thread current = Thread.currentThread();
    while(!sign .compareAndSet(null, current)){
    }
  }
  public void unlock (){
    Thread current = Thread.currentThread();
    sign .compareAndSet(current, null);
  }
}
```

由于自旋锁只是将当前线程不停地执行循环体，不进行线程状态的改变，所以响应速度更快。但当线程数不停增加时，性能下降明显，因为每个线程都需要执行，占用CPU时间。如果线程竞争不激烈，并且保持锁的时间段。适合使用自旋锁。

在自旋锁中,另有三种常见的锁形式:TicketLock ，CLHlock 和MCSlock
Ticket锁主要解决的是访问顺序的问题，主要的问题是在多核cpu上,每次都要查询一个serviceNum 服务号，影响性能（必须要到主内存读取，并阻止其他cpu修改）。

CLHlock是不停的查询前驱变量， 导致不适合在NUMA 架构下使用（在这种结构下，每个线程分布在不同的物理内存区域）。

MCSLock则是对本地变量的节点进行循环。不存在CLHlock 的问题。


* 阻塞锁
阻塞锁可以说是让线程进入阻塞状态进行等待，当获得相应的信号（唤醒，时间） 时，才可以进入线程的准备就绪状态，准备就绪状态的所有线程，通过竞争，进入运行状态。
与自旋锁不同，它改变了线程的运行状态。

``` java
public class CLHLock1 {
 public static class CLHNode {
     private volatile Thread isLocked;
 }

 @SuppressWarnings("unused")
 private volatile CLHNode                                            tail;
 private static final ThreadLocal<CLHNode>                           LOCAL   = new ThreadLocal<CLHNode>();
 private static final AtomicReferenceFieldUpdater<CLHLock1, CLHNode> UPDATER = AtomicReferenceFieldUpdater.newUpdater(CLHLock1.class,CLHNode.class, "tail");

 public void lock() {
     CLHNode node = new CLHNode();
     LOCAL.set(node);
     CLHNode preNode = UPDATER.getAndSet(this, node);

     if (preNode != null) {
         preNode.isLocked = Thread.currentThread();
         LockSupport.park(this);
         preNode = null;
         LOCAL.set(node);
     }
 }

 public void unlock() {
     CLHNode node = LOCAL.get();
     if (!UPDATER.compareAndSet(this, node, null)) {
         System.out.println("unlock\t" + node.isLocked.getName());
         LockSupport.unpark(node.isLocked);
     }
     node = null;
 }
}

```

阻塞锁的优势在于，阻塞的线程不会占用cpu时间， 不会导致 CPu占用率过高，但进入时间以及恢复时间都要比自旋锁略慢。

* 可重入锁
可重入锁，也叫做递归锁，指的是同一线程 外层函数获得锁之后 ，内层递归函数仍然有获取该锁的代码，但不受影响。
在JAVA中 ReentrantLock 和synchronized 都是可重入锁

可重入锁最大的作用是避免死锁

## synchronized 和 lock ##
synchronized 是JVM层提供的同步技术，与lock不同，synchronized是一种不可中断的锁，利用lock的可中断性，我们可以在开发中释放一个被占用的锁。

## Lock 接口##

{% img Lock接口概览图 /images/note-about-java-lock.png  %}
{% img Lock接口概览图 /images/note-about-java-lock-impl.png %}

## 参考 ##
[java锁的种类以及辨析（一）：自旋锁](http://ifeve.com/java_lock_see1/)
[Java锁的种类以及辨析（二）：自旋锁的其他种类：自旋锁](http://ifeve.com/java_lock_see2/)
[Java锁的种类以及辨析（三）：阻塞锁：自旋锁](http://ifeve.com/java_lock_see3/)
[Java锁的种类以及辨析（四）：可重入锁：自旋锁](http://ifeve.com/java_lock_see4/)
[Java并发编程：Lock](http://www.cnblogs.com/dolphin0520/p/3923167.html)
