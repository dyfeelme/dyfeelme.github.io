---
title: XQuery学习笔记
tags:
  - xml
categories:
  - xml
date: 2014-11-13 10:48:08
---
[XQuery](http://www.w3school.com.cn/xquery/index.asp)是一门用来检索XML的语言，类似于SQL于关系型数据库，通过XQuery可以对XML文档进行帅选和查找。 因为XQuery以XPath为基础，所以还未了解XPath的同学请移步作者另一篇博文[XPath学习笔记]()。
<!-- more -->

## 语法 ##
一些基本的语法规则：

* 大小写敏感
* 元素、属性以及变量必须是合法的 XML 名称。
* 字符串值可使用单引号或双引号。
* 变量由 “$” 并跟随一个名称来进行定义，举例，$bookstore
* 注释被 (: 和 :) 分割，例如，(: XQuery 注释 :)

## XQuery in Action ##
按照惯例，我们直接通过实例来操作，如下：
``` xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<bookstore>

<book category="COOKING">
  <title lang="en">Everyday Italian</title>
  <author>Giada De Laurentiis</author>
  <year>2005</year>
  <price>30.00</price>
</book>

<book category="CHILDREN">
  <title lang="en">Harry Potter</title>
  <author>J K. Rowling</author>
  <year>2005</year>
  <price>29.99</price>
</book>

<book category="WEB">
  <title lang="en">XQuery Kick Start</title>
  <author>James McGovern</author>
  <author>Per Bothner</author>
  <author>Kurt Cagle</author>
  <author>James Linn</author>
  <author>Vaidyanathan Nagarajan</author>
  <year>2003</year>
  <price>49.99</price>
</book>

<book category="WEB">
  <title lang="en">Learning XML</title>
  <author>Erik T. Ray</author>
  <year>2003</year>
  <price>39.95</price>
</book>

</bookstore>

* doc() 用于打开 "books.xml" 文件

``` xml
doc("books.xml")
```

* 使用XPath路径表达式在 "books.xml" 文件中选取所有的 title 元素

``` xml
doc("books.xml")/bookstore/book/title

结果：
<title lang="en">Everyday Italian</title>
<title lang="en">Harry Potter</title>
<title lang="en">XQuery Kick Start</title>
<title lang="en">Learning XML</title>
```

* 选取 bookstore 元素下的所有 book 元素，并且所选取的 book 元素下的 price 元素的值必须小于 30

``` xml
doc("books.xml")/bookstore/book[price<30]

结果：
<book category="CHILDREN">
  <title lang="en">Harry Potter</title>
  <author>J K. Rowling</author>
  <year>2005</year>
  <price>29.99</price>
</book>
```

## FLOWER ##
FLWOR 是 "For, Let, Where, Order by, Return" 的首字母缩写。

* for 语句把 bookstore 元素下的所有 book 元素提取到名为 $x 的变量中。
* let 用于定义变量。
* where 语句选取了 price 元素值大于 30 的 book 元素。
* order by 语句定义了排序次序。将根据 title 元素进行排序。
* return 语句规定返回什么内容。在此返回的是 title 元素。

所以如下两种方式均可得到同样的结果：

``` xquery
doc("books.xml")/bookstore/book[price>30]/title
```
等同于：
``` xquery
for $x in doc("books.xml")/bookstore/book
where $x/price>30
return $x/title
```
结果：
``` xml
<title lang="en">XQuery Kick Start</title>
<title lang="en">Learning XML</title>
```

## 表达式 ##

* 条件表达式If-Then-Else

"If-Then-Else" 的语法：
if 表达式后的圆括号是必需的。
else 也是必需的，不过只写 “else ()” 也可以。

``` xquery
for $x in doc("books.xml")/bookstore/book
return	if ($x/@category="CHILDREN")
	then <child>{data($x/title)}</child>
	else <adult>{data($x/title)}</adult>
```

* 比较

在 XQuery 中，有两种方法来比较值。
通用比较：=, !=, <, <=, >, >=
值的比较：eq、ne、lt、le、gt、ge

如下：

``` xquery
$bookstore//book/@q > 10
```
等同于：
``` xquery
$bookstore//book/@q gt 10
```
注：以上示例均来自于W3CSchool官方教程，[更多参考](http://www.w3school.com.cn/xquery)

## 总结 ##

XQuery还提供函数操作等高级操作，同XPath结合使用,可高效而简洁的对XML数据进行查找，过滤，排序和组装。

## 参考 ##
[W3CSchool XQuery 教程](http://www.w3school.com.cn/xquery/)
