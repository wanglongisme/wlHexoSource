---
layout: post
title: jdk的native2ascii工具
comments: false
categories:
  - 随笔
tags:
  - 2017
abbrlink: f4dc1819
date: 2017-02-14 11:36:14
---

国际化的资源文件只能包含ASC码的字符,所以写中文需要unicode的表示方式,在开发中会有不便.JDK的bin目录提供一个ative2ascii的工具可以将中文字符的资源文件转换成Unicode编码的文件.
命令格式:
native2ascii [-reverse] [-encoding 编码] [输入文件 [输出文件]]
示例:
d:\&gt;native2ascii -encoding utf-8 d:\resource_zh_CN.properties d:\resource_zh_CN_1.properties
资源文件采用utf-8格式, 所以必须显式指定编码.
#IDE中都有资源文件属性编辑器的插件,会自动将内容转换成ASC码的表示,同时不影响阅读和编辑.
