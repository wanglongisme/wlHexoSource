---
layout: post
title: java反射_方法_java.lang.reflect.Method
comments: false
categories:
  - 随笔
tags:
  - 2017
abbrlink: 78f9635
date: 2017-03-22 11:41:00
---

Class rabbitClass = Rabbit.class;
Method[] rabbitMethodArr = rabbitClass.getMethods();
通过class对象获取所有public的方法对象
----------------------------------------------------
获取指定方法对象
Method method = rabbitClass.getMethod("rap",new Class[]{String.class});
Method method = rabbitClass.getMethod("rap",null); //方法没有参数
没有找到会抛出NoSuchMethodException.
----------------------------------------------------
方法参数
Class[] paramTypeArr = method.getParameterTypes();
返回类型
Class returnClass = method.getReturnType();
----------------------------------------------------
调用方法
Object returnValue = method.invoke(null, "8 mile"); //静态方法传null
Object returnValue = method.invoke(new Rabbit(), "8 mile"); //非静态方法需要传入class对象的实例.

