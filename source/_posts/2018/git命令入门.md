---
layout: post
title: git命令入门
comments: false
categories:
  - 随笔
  - 2018
abbrlink: bf2b1827
date: 2018-01-05 11:48:56
tags:
 - git
---
>只是简单的记录了命令和解释.
>各命令使用场景和详细可以参考: [git命令](http://wiki.jikexueyuan.com/project/git-tutorial/version-back.html)

`git init` 将当前目录声明为git仓库
`git add filename` 将文件添加到仓库
`git commit -m "注释"` 将添加过的文件commit,多个文件.
`git status` 查看当前仓库状态
`git diff`` 查看仓库文件修改信息
`git log` 查看版本历史记录
<!--more-->
```
H:\gitRes>git log --pretty=oneline
b8ddc184923dd5d01508ed55cb6392416aaaa18f (HEAD -> master) test   //HEAD表示当前版本
d7a7fd75f79344f7d9e7921475aa1d8fd0cb5c16 update 1 line
4d80107cd38a9e353076adaedb6248ff4572d7f0 add a test.txt
```
`git reset --hard 版本id`  //回退到一个版本,id可以不用写全保证唯一位数即可
```
H:\gitRes>git reset --hard b8ddc
HEAD is now at b8ddc18 test
```
`git reflog`查看之前执行命令,如果回退到之前版本,又想回到现在版本时,`git log`已经看不到id了,可以通过该命令查看.

git有个[暂存区](http://wiki.jikexueyuan.com/project/git-tutorial/workspace-and-staging-area.html)的概念比较重要.

---
**为什么 Git 比其他版本控制系统设计得优秀，因为 Git 跟踪并管理的是修改，而非文件**
`git diff HEAD -- test.txt`查看test.txt在工作区和版本库里的区别
```
H:\gitRes>git diff
diff --git a/test.txt b/test.txt
index cc3e949..b893c83 100644
--- a/test.txt
+++ b/test.txt
@@ -7,3 +7,4 @@ git is a free.

 aaaa2018-01-05 13:55:51
 1111111
+2222222
```
`git checkout -- test.txt`撤销修改, 就是让这个文件回到最近一次`git commit`或`git add`时的状态。**注--很重要**
`git reset HEAD test.txt`从暂存区撤回, 把暂存区的修改撤销掉（unstage），重新放回工作区
>git reset 命令既可以回退版本,也可以把暂存区的修改回退到工作区.

当删除了工作区的文件时,
1.`git status`命令会显示哪些命令删除了,可以使用`git rm test.txt` `git commit -m `删除文件
2.如果删错了,想恢复`git checkout -- test.txt`
`git checkout`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。