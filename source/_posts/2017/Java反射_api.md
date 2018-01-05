---
layout: post
title: Java反射_api
comments: false
categories:
  - 随笔
tags:
  - 2017
abbrlink: a57a3144
date: 2017-03-22 10:44:57
---

获取Class对象的两种方式:
Class rabbitClass = Rabbit.class;
Class rabbitClass = Class.forName("com.xxx.Rabbit");
如果Class.forName()没有找到该类则会抛出ClassNotFoundException.
------------------------------------
class对象获取类名
rabbitClass.getName(); //获取全类名
rabbitClass.getSimpleName(); //获取类名
------------------------------------
获取class对象访问修饰符
int modifiers = rabbitClass.getModifiers(); //修饰符被包装成int类型,可以用java.lang.reflect.Modifier检查.
------------------------------------
获取class对象包信息
Package package = rabbitClass.getPackage();
------------------------------------
获取父类class对象
Class fatherClass = rabbitClass.getSuperClass();
------------------------------------
class对象实现的接口
Class[] interfaceArr = rabbitClass.getInterfaces(); //并不会返回父类实现的接口,尽管当前类已经实现了父接口.
------------------------------------
class对象的构造方法
Constructor[] rabbitConstructorArr = rabbitClass.getConstructors();
------------------------------------
获取方法
Method[] rabbitMethodArr = rabbitClass.getMethods();
------------------------------------
成员变量
Field[] rabbitFieldArr = rabbitClass.getFields();
------------------------------------
class对象的注解
Annotation[] rabbitAnnotationArr = rabbitClass.getAnnotations();
