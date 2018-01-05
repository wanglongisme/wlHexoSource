---
layout: post
title: Java反射_变量_java.lang.reflect.Field
comments: false
categories:
  - 随笔
tags:
  - 2017
abbrlink: 4800e2ad
date: 2017-03-22 11:13:47
---

Class rabbitClass = Rabbit.class;
//获取rabbitClass的所有public的变量
Field[] rabbitClassFieldArr = rabbitClass.getFields();
---------------------------------------------------------------
通过变量名,获取具体的变量对象
Field field = rabbitClass.getField("name");
如果没有找到,抛出NoSuchFieldException.
---------------------------------------------------------------
通过Field对象获取变量名称
String fieldName = field.getName();
---------------------------------------------------------------
通过Field对象获取变量类型
Object fieldType = field.getType();
---------------------------------------------------------------
get/set变量值
Rabbit rabbit = new Rabbit();
//get()和set()方法需要传入拥有该变量对象的实例
Object value = field.get(rabbit);
field.set(rabbit,"newName");
//如果是静态变量public static 可以传入null或传入对象.
