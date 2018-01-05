---
layout: post
title: mysql的8小时问题
comments: false
categories:
  - 随笔
tags:
  - 2017
abbrlink: 18a7eda1
date: 2017-03-16 16:00:37
---

  前些天用spring得task做了个定时任务,这几天发现没每天都不可用,会报一个connection失败的异常.刚才看书提到一个mysql的8小时问题.感觉就是它了.
  mysql有一个最大空闲时间的设置,默认8小时.当一个连接空闲超过8小时将不可用,应用程序使用时就会报错获取不到connection.如果dbcp连接方式,可以设置testOnBorrow=true,每次使用连接时都判断该连接是否可用,如果不可用重新获取.这种方法比较耗费性能.另一种是将testOnBorrow=false,testWhileIdle=true,再设置timeBetweenEvictionRunsMillis的值.这样dbcp有一个后台线程用来定时检测过空闲的连接会销毁.只要时间小于8小时即可.
