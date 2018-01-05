---
layout: post
title: spring的ReloadableResourceBundleMessageSource定时刷新资源文件
comments: false
categories:
  - 随笔
tags:
  - 2017
abbrlink: 6786b4ba
date: 2017-02-14 11:58:23
---

spring为了方便国际化的使用,提供了一个ReloadableResourceBundleMessageSource的实现类,该类与ResourceBundleMessageSource的区别是可以定时的刷新资源文件而不需要重新启动服务器.
<pre>
  <bean id="myResource" class="org.springframework.context.support.ReloadableResourcesBundleMessageSource">
    <property name="basenames"> 
      <list>    
        <value>com/test/i18n/fmt_resource</value>
      </list>
    </property>
    <property name="cacheSeconds" value="5" ></property>
  </bean>
</pre>
通过cacheSeconds属性控制资源文件5秒钟刷新一次,但频繁的刷新会影响性能,所以建议大于30分钟,但值为-1是表示不刷和ResourceBundleMessageSource类功能相同.
</br>
