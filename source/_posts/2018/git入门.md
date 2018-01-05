---
layout: post
title: git入门
comments: false
categories:
  - 随笔
  - 2018
tags:
  - git
abbrlink: c8c37a7
date: 2018-01-05 10:20:00
---

github注册，创建仓库不在记录，网上很多，就记下自己配置brach的情况。
>电脑环境: win7 64bit. 

1.首先在github上对感兴趣的项目fork一下,然后在自己的githug上就会看到该项目.

2.复制仓库到本地
```
git clone https://github.com/xxx/Spoon-Knife
//命令执行后,会在本地生成对应目录.
```
3.cd命令进入目录
```
git remove -v
//查看远程仓库位置
```

<!--more-->
4.添加远程仓库upstream位置,也就是项目拥有人的github地址.
```
git remote add upstream https://github.com/octocat/Spoon-Knife.git
//再次查看git remote -v  会发现多了2个upstream地址
```
5.从原始库中获取分支和它们各自的提交
```
git fetch upstream
```
6.切换分支
```
git checkout master 
```
7.将原始库中更改,同步到本地分支中
```
git merge upstream / master 
```
刚接触git,看的比较慢.使用中,逐渐熟悉吧.



