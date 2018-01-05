---
layout: post
title: Java反射_构造方法_java.lang.reflect.Constructor
comments: false
categories:
  - 随笔
tags:
  - 2017
abbrlink: be6929de
date: 2017-03-22 10:58:43
---

Class rabbitClass = RabbitClass.class;
Contructor[] rabbitContructorArr = rabbitClass.getContructors();
该方法返回Rabbit类对象的所有public的构造方法.
---------------------------------------------------------------
Constructor rabbitConstructor = rabbitClass.getConstructor(new Class[]{String.class});
获取指定参数的构造方法,如果没找到抛出NoSuchMethodException.
---------------------------------------------------------------
获取构造方法对象的方法参数信息
Class[] paramTypeArr = rabbitConstructor.getParameterTypes();
---------------------------------------------------------------
通过构造方法class对象实例化类
Rabbit rabbitObj = rabbitConstructor.newInstance("Eminem");


