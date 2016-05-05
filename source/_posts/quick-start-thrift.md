---
title: Thrift入门
tags:
  - java
  - thrift
  - rpc
categories:
  - java
  - rpc
date: 2015-03-11 15:37:03
---

本章介绍服务调用的第三种方式：RPC（Remote Protcal Call）,详见[常用服务调用方式](http://??),本节主要介绍基于Apache Thrift来实现RPC的调用。
![thrift 架构图](/images/quick-start-thrift-architecture.jpg)
<!-- more -->

## 安装 ##

## 协议 ##
* Transport层提供了一个简单的网络读写抽象层，有阻塞与非阻塞的TCP实现与HTTP的实现。

* Protocol层定义了IDL中的数据结构与Transport层的传输数据格式之间的编解码机制。传输格式有二进制，压缩二进制，JSON等格式，IDL中的数据结构则包括Message，Struct，List，Map，Int，String，Bytes等。

* Processor层由编译器编译IDL文件生成。
生成的代码会将传输层的数据解码为参数对象(比如商品对象有id与name两个属性，生成的代码会调用Protocol层的readInt与readString方法读出这两个属性值)，然后调用由用户所实现的函数，并将结果编码送回。

## IDL介绍 ##
接口定义语言（Interface Definition Language）,简称IDL。

* 支持的类型：

``` java
bool        Boolean, one byte
i8 (byte)   Signed 8-bit integer
i16         Signed 16-bit integer
i32         Signed 32-bit integer
i64         Signed 64-bit integer
double      64-bit floating point value
string      String
binary      Blob (byte array)
map<t1,t2>  Map from one type to another
list<t1>    Ordered list of one type
set<t1>     Set of unique elements of one type
```

* 导入外部thrift

``` java
include "shared.thrift"
```

* 命名空间

``` java
namespace cpp tutorial
namespace d tutorial
namespace dart tutorial
namespace java tutorial
namespace php tutorial
namespace perl tutorial
namespace haxe tutorial
```

* 定义类型

``` java
typedef i32 MyInteger
```

* 产量

``` java
const i32 INT32CONSTANT = 9853
const map<string,string> MAPCONSTANT = {'hello':'world', 'goodnight':'moon'}
```

* 枚举

``` java
enum Operation {
  ADD = 1,
  SUBTRACT = 2,
  MULTIPLY = 3,
  DIVIDE = 4
}

```

* 结构

``` java
struct Work {
  1: i32 num1 = 0,
  2: i32 num2,
  3: Operation op,
  4: optional string comment,
}
```

* 异常

``` java
exception InvalidOperation {
  1: i32 whatOp,
  2: string why
}
```

* 定义服务

``` java
service Calculator extends shared.SharedService {

  /**
   * A method definition looks like C code. It has a return type, arguments,
   * and optionally a list of exceptions that it may throw. Note that argument
   * lists and exception lists are specified using the exact same syntax as
   * field lists in struct or exception definitions.
   */

   void ping(),

   i32 add(1:i32 num1, 2:i32 num2),

   i32 calculate(1:i32 logid, 2:Work w) throws (1:InvalidOperation ouch),

   /**
    * This method has a oneway modifier. That means the client only makes
    * a request and does not listen for any response at all. Oneway methods
    * must be void.
    */
   oneway void zip()

}
```

## 命令 ##

``` bash
thrift --gen <language> <Thrift filename>		#生成指定语言的代码
thrift -r --gen <language> <Thrift filename>
```

## hello ##

``` java
namespace java service.demo 
 service Hello{ 
  string helloString(1:string para) 
  i32 helloInt(1:i32 para) 
  bool helloBoolean(1:bool para) 
  void helloVoid() 
  string helloNull() 
 }
```

## 参考 ##
[Thrift IDL](http://thrift.apache.org/docs/idl)
[花钱的年华](http://calvin1978.blogcn.com/articles/apache-thrift.html)