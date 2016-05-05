---
title: Java 并发包解析
tags:
  - java
categories:
  - java
date: 2015-12-04 12:44:12
---

JDK1.5以后新增了java.util.concurrent，俗称并发包，涵盖和可用于支持多线程并发解决方案的多种工具集合。
<!-- more -->

## Feature接口 ##

* boolean cancel(boolean mayInterruptIfRunning); 
	尝试取消一个正在执行的任务，如果任务不能被取消或者已经正确的完成，返回False,否则返回True
* boolean isCancelled();
	判断任务是否在完成前成功被取消
* boolean isDone();
	判断任务是否已经完成
* V get() throws InterruptedException, ExecutionException;
	必要的时候等待任务计算完成后接收返回结果
* V get(long timeout, TimeUnit unit) throws InterruptedException, ExecutionException, TimeoutException;
	在指定时间内等待任务计算完成后返回结果

Feature接口设计用来处理并发模式中的数据流，还有两种比较常见的并发设计模式：

* 基于回调驱动 (多线程)
* 消息事件驱动（Actor模型）

## Executors 类 ##
多线程编程中可以通过Executor根据需要创建不同的线程池。Executors本身算是一个工厂类

* FixedThreadPool 创建一个固定大小的线程池，有两种方法签名：
``` java
ExecutorService newFixedThreadPool(int nThreads)
ExecutorService newFixedThreadPool(int nThreads, ThreadFactory threadFactory)
```

* WorkStealingPool JDK1.8以后增加的方法，可以根据并行级别创建适配ForkJoin模式的线程，有两种方法签名：
``` java
ExecutorService newWorkStealingPool()
ExecutorService newWorkStealingPool(int parallelism) 
```

* SingleThreadExecutor 创建一个内部使用LinkedBlockingQueue作为队列的单一线程，有两种方法签名：
``` java
ExecutorService newSingleThreadExecutor()
ExecutorService newSingleThreadExecutor(ThreadFactory threadFactory)
```

* CachedThreadPool 创建一个动态大小的线程池，有两种方法签名：
``` java
ExecutorService newCachedThreadPool()
ExecutorService newCachedThreadPool(ThreadFactory threadFactory)
```

* SingleThreadScheduledExecutor 创建一个支持计划任务的单一线程，有两种方法签名：
``` java
ScheduledExecutorService newScheduledThreadPool(int corePoolSize)
ScheduledExecutorService newScheduledThreadPool(int corePoolSize, ThreadFactory threadFactory)
```


## ForkJoinTask 类 ##
JDK1.7加入了并行编程来支持多核计算，Fork/Join模式主要适用于：
如果一个复杂的计算任务可以由拆分开的子任务计算结果重新组合而成的情况。
ForkJoinTask是一个抽象类，包含了许多方法，通常我们需要根据实际情况继承他的子类，如下：
{% img ForkJoinTask子类概览  /images/note-about-java-concurrent-fork-join-task.png 300 550%}
如上：

* RecursiveAction 是继承自ForkJoinTask的抽象类，它不需要返回值，当子任务都执行完毕之后，不需要进行中间结果的组合。
* RecursiveTask 也是一个继承自ForkJoinTask的抽象类，不同于RecursiveAction，他可以指定一个泛型的返回值，并且可以使用 finish() 方法显式中止的 AsyncAction 和 LinkedAsyncAction，以及可使用 TaskBarrier 为每个任务设置不同中止条件的 CyclicAction。
* CyclicAction 如果我们有一个复杂任务需要几个线程协作完成，并且线程之间需要在某个点等待所有其他线程到达，那么就能用 CyclicAction 和 TaskBarrier 来完成


