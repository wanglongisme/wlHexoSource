---
layout: post
title: java反射_私有变量和私有方法
comments: false
categories:
  - 随笔
tags:
  - 2017
abbrlink: 7c42fd9e
date: 2017-03-22 12:08:14
---

反射操作私有变量
Rabbit rabbit = new Rabbit("Eminem");
Field privateField = Rabbit.class.getDeclaredField("privateName");
privateField.setAccessible(true); 
//关闭Field实例的反射访问检查,执行后不论私有,受保护,包访问作用域,都可以访问,即使不在访问权限作用域内.
String value = (String)privateField.get(rabbit);
System.out.print("[privateName="+value+"]"); //输出 [privateName=Eminem]
--------------------------------------------------------------------------------------------
反射操作私有方法
Rabbit rabbit = new Rabbit("Eminem");

Method privateMethod = Rabbit.class.getDeclaredMethod("getPrivateName", null);
privateMethod.setAccessible(true);
String returnValue = privateMethod.invoke(rabbit, null); //如果方法又返回值
System.out.print(returnValue);

