---
title: Java模板引擎-Beetl
tags:
  - java
categories:
  - java
date: 2015-08-04 18:22:32
---

## 简介 ##
{% blockquote Beetl %}
[Beetl](http://ibeetl.com/guide/beetl.html)是新一代的Java模板引擎，简单易学，超高性能，并且易于整合和扩展。
{% endblockquote %}

## 用法 ##
Beetl的核心是GroupTemplate，创建GroupTemplate需要俩个参数，一个是模板资源加载器，一个是配置类，模板资源加载器Beetl内置了4种，分别是

* StringTemplateResourceLoader：字符串模板加载器，用于加载字符串模板，如本例所示
* FileResourceLoader：文件模板加载器，需要一个根目录作为参数构造，，传入getTemplate方法的String是模板文件相对于Root目录的相对路径
* ClasspathResourceLoader：文件模板加载器，模板文件位于Classpath里
* WebAppResourceLoader：用于webapp集成，假定模板根目录就是WebRoot目录，参考web集成章
* MapResourceLoader : 可以动态存入模板

## 配置 ##
``` xml

#默认配置
#配置引擎实现类
ENGINE=org.beetl.core.engine.FastRuntimeEngine
#指定了占位符号，默认是${ }.也可以指定为其他占位符。
DELIMITER_PLACEHOLDER_START=${
DELIMITER_PLACEHOLDER_END=}
#指定了语句的定界符号，默认是<% %>,也可以指定为其他定界符号
DELIMITER_STATEMENT_START=<%
DELIMITER_STATEMENT_END=%>
#指定IO输出模式，默认是FALSE,即通常的字符输出，在考虑高性能情况下，可以设置成true。
DIRECT_BYTE_OUTPUT = FALSE
#指定了支持HTML标签，且符号为#,默认配置下，模板引擎识别<#tag ></#tag>这样的类似html标签，并能调用相应的标签函数或者模板文件。你也可以指定别的符号，如bg: 则识别<bg:
HTML_TAG_SUPPORT = true
HTML_TAG_FLAG = #
#指定如果标签属性有var，则认为是需要绑定变量给模板的标签函数
HTML_TAG_BINDING_ATTRIBUTE = var
#指定允许本地Class直接调用
NATIVE_CALL = TRUE
#指定模板字符集是UTF-8
TEMPLATE_CHARSET = UTF-8
#指定异常的解析类，默认是ConsoleErrorHandler，他将在render发生异常的时候在后台打印出错误信息（System.out)。
ERROR_HANDLER = org.beetl.core.ConsoleErrorHandler
#指定了本地Class调用的安全策略
NATIVE_SECUARTY_MANAGER= org.beetl.core.DefaultNativeSecurityManager
#配置了是否进行严格MVC，通常情况下，此处设置为false.
MVC_STRICT = FALSE
#资源配置，resource后的属性只限于特定ResourceLoader
RESOURCE_LOADER=org.beetl.core.resource.ClasspathResourceLoader
#classpath 根路径
RESOURCE.root= /
#是否检测文件变化
RESOURCE.autoCheck= true
#自定义脚本方法文件的Root目录和后缀
RESOURCE.functionRoot = functions
RESOURCE.functionSuffix = html
#自定义标签文件Root目录和后缀
RESOURCE.tagRoot = htmltag
RESOURCE.tagSuffix = tag

#####  扩展 ##############
## 内置的方法
FN.date = org.beetl.ext.fn.DateFunction
##内置的功能包
FNP.strutil = org.beetl.ext.fn.StringUtil
##内置的默认格式化函数
FTC.java.util.Date = org.beetl.ext.format.DateFormat
## 标签类
TAG.include= org.beetl.ext.tag.IncludeTag
```

## 集成Spring ##
重写BeetlSpringView类
``` java
import java.util.Locale;
import org.beetl.ext.spring.BeetlGroupUtilConfiguration;
import org.beetl.ext.spring.BeetlSpringView;

public class RichBeetlSpringView extends BeetlSpringView {

/**
 * 重写验证模板资源
 */
@Override
public boolean checkResource(Locale locale) throws Exception {
    BeetlGroupUtilConfiguration config = getApplicationContext().getBean(BeetlGroupUtilConfiguration.class);
    return config.getGroupTemplate().getResourceLoader().exist(getUrl());
}
}
```
接下来配置Spring
``` xml
<bean id="beetlConfig" class="org.beetl.ext.spring.BeetlGroupUtilConfiguration" init-method="init"/>

<!-- Beetl视图解析器1 *.btl -->
<bean id="beetlViewResolver" class="org.beetl.ext.spring.BeetlSpringViewResolver">
    <property name="viewClass" value="com.holdtime.framework.beetl.tagext.RichBeetlSpringView"/>
    <property name="contentType" value="text/html;charset=UTF-8" />
    <property name="prefix" value="/WEB-INF/pages/" />
    <property name="suffix" value=".btl"></property>
    <property name="order" value="0"/>
</bean>

<!-- Beetl视图解析器2 *.html -->
<bean id="htmlViewResolver" class="org.beetl.ext.spring.BeetlSpringViewResolver">
    <property name="viewClass" value="com.holdtime.framework.beetl.tagext.RichBeetlSpringView"/>
    <property name="contentType" value="text/html;charset=UTF-8" />
    <property name="prefix" value="/WEB-INF/pages/" />
    <property name="suffix" value=".html"></property>
    <property name="order" value="1"/>
</bean>

```