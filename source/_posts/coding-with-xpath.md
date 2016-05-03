---
title: XPath学习笔记
tags:
  - xml
categories:
  - xml
date: 2014-11-08 10:19:01
---


## 概述 ##
[XPath](http://www.w3school.com.cn/xpath/index.asp) 是一门在 XML 文档中查找信息的语言。通过类似于路径的方式来达到定位和查找元素的目的。

## 术语 ##
* _节点（Node）_,文档有七种类型的节点：元素、属性、文本、命名空间、处理指令、注释以及文档（根）节点。
* _基本值（或称原子值，Atomic value）_,是无父或无子的节点，如:Hello，"Hello",3等
* _项目（Item）_,是基本值和节点的统称。
* _节点关系_
	* 父（Parent）,每个元素以及属性都有一个父。
	* 子（Children）,元素节点可有零个、一个或多个子。
	* 同胞（Sibling）,拥有相同的父的节点
	* 先辈（Ancestor）,某节点的父、父的父，等等。
	* 后代（Descendant）,某个节点的子，子的子，等等。
众所周知，XML 文档是被作为节点树来对待的。树的根被称为文档节点或者根节点。

## 选取 ##
{% img XPath选取 /images/howto-use-xpath.png 400 300 %}
如上，我们可以使用路径表达式来对要选取的元素进行查找和定位。下面我们将通过实例来进行讲解：

## XPath in Action ##
``` xml
<?xml version="1.0" encoding="utf-8"?>
<bookstore>
<book>
  <title lang="eng">Learning XPath</title>
  <author>w3cschool</author>
  <price>29.99</price>
</book>

<book>
  <title lang="zh">深入学习Java</title>
  <author>dyfeelme</author>
  <price>89.99</price>
</book>
</bookstore>
```

* 匹配任何元素节点。
``` xml
*
```

* 匹配任何属性节点。
``` xml
@*
```

* 匹配任何类型的节点。
``` xml
node()
```

* 选取所有book结点
``` xml
book
```

* 选取根节点bookstore
``` xml
/bookstore
```

* 查找所有book结点
``` xml
//book
book
```

* 查找选取所有根节点bookstore下的book结点
``` xml
/bookstore//book
```

* 选取所有名为lang的属性
``` xml
//@lang
```

* 选取属于 bookstore 子元素的第一个 book 元素
``` xml
/bookstore/book[1]
```

* 选取属于 bookstore 子元素的最后一个 book 元素。
``` xml
/bookstore/book[last()]
```

* 选取属于 bookstore 子元素的倒数第二个 book 元素。
``` xml
/bookstore/book[last()]
```

* 选取最前面的两个属于 bookstore 元素的子元素的 book 元素。
``` xml
/bookstore/book[position()<3]
```

* 选取所有拥有名为 lang 的属性的 title 元素。
``` xml
//title[@lang]
```

* 选取所有 title 元素，且这些元素拥有值为 eng 的 lang 属性。
``` xml
//title[@lang='eng']
```

* 选取 bookstore 元素的所有 book 元素，且其中的 price 元素的值须大于 35.00。
``` xml
/bookstore/book[price>35.00]
```

* 选取 bookstore 元素中的 book 元素的所有 title 元素，且其中的 price 元素的值须大于 35.00。
``` xml
/bookstore/book[price>35.00]/title
```

* 选取 book 元素的所有 title 和 price 元素。
``` xml
//book/title | //book/price
```
XPath还提供运算符，如'+','-','*','\','>',or','and'等，以及各种内置函数。

注：以上示例均选自W3CSchool官方教程，[更多参考](http://www.w3school.com.cn/xpath)

## 参考 ##
[W3CSchool XPath 教程](http://www.w3school.com.cn/xpath/)