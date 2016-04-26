---
title: 关于Spring整合Quartz的问题
tags:
  - stackoverflow
  - spring
  - quartz
categories:
  - stackoverflow
  - quartz
date: 2016-04-26 20:03:56
---


## 问题描述 ##
Caused by: Java.lang.IncompatibleClassChangeError: class org.springframework.scheduling.quartz.CronTriggerBean has interface org.quartz.CronTrigger as super class

## 解决方法 ##
如上问题，一般是由于spring 3.x 和 quartz 2.X版本不兼容导致，具体原因是org.quartz.CronTrigger在2.0以后从class变成了一个接口导致，坑啊，所以说前期设计架构一定要搞好啊。
trigger 用 org.springframework.scheduling.quartz.CronTriggerFactoryBean
``` xml
<!-- 基于Cron表达式的打火器 -->
<bean id="cronTrigger"
	class="org.springframework.scheduling.quartz.CronTriggerFactoryBean">
	<property name="jobDetail" ref="jobDetail" />
	<!-- 每分钟执行一次 -->
	<property name="cronExpression" value="*/30 * * * * ?" />
</bean>
```

上述问题还有可能存在于Tomcat版本不兼容的问题上，比如tomcat-7.0.16中发现会有上述的问题。

## 问题描述 ##
Caused by: java.io.IOException: JobDataMap values must be Strings when the 'useProperties' property is set.  Key of offending value: methodInvoker

## 解决方法 ##
如下：
``` java

```

## 问题描述 ##
不能通过依赖注入的方式直接获取bean实例

## 解决方法 ##
1. 在Job中通过预先注入好的实例，ApplicationContext.getBean("xxx")获取。
2. 重写 JobBeanFactory,通过配置SchedulerFactoryBean来指定自定义的FactoryBean,如下：

``` xml
<bean class="org.springframework.scheduling.quartz.SchedulerFactoryBean">

	...此处省略

	<property name="jobFactory">
		<bean class="com.xxx.AutowiredSpringBeanJobFactory" />
	</property>
</bean>
```

``` java
import org.quartz.spi.TriggerFiredBundle;
import org.springframework.beans.BeansException;
import org.springframework.beans.factory.config.AutowireCapableBeanFactory;
import org.springframework.context.ApplicationContext;
import org.springframework.context.ApplicationContextAware;
import org.springframework.scheduling.quartz.SpringBeanJobFactory;

public class AutowiredSpringBeanJobFactory  extends SpringBeanJobFactory implements ApplicationContextAware{

	private AutowireCapableBeanFactory factory;
	
	@Override
	public void setApplicationContext(ApplicationContext context) throws BeansException {
		factory = context.getAutowireCapableBeanFactory();
	}
	
	@Override
	protected Object createJobInstance(TriggerFiredBundle bundle) throws Exception {
		 final Object instance = super.createJobInstance(bundle);
	     factory.autowireBean(instance);
	     return instance;
	}

}
```

