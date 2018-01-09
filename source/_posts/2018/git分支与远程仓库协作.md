---
layout: post
title: git分支与远程仓库协作
comments: false
categories:
  - 随笔
abbrlink: bfdc69d7
date: 2018-01-08 11:32:50
tags:
 - git
---

>当使用git克隆时，其实是git自动把本地master与远程仓库master关联起来，远程仓库默认名为origin。

查看远程仓库信息
`git remote -v` 显示远程库名称、路径、权限，当前拥有fetch和push权限。
```
H:\wlHexo>git remote -v
origin  git@github.com:wanglongisme/wlHexoSource.git (fetch)
origin  git@github.com:wanglongisme/wlHexoSource.git (push)
```
>推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git 就会把该分支推送到远程库对应的远程分支上。 	
> `git push origin master`
> 如果要推送其他分支，比如 dev，就改成：
> `git push origin dev`
> 但是，并不是一定要把本地分支往远程推送，那么，哪些分支需要推送，哪些不需要呢？
> * master 分支是主分支，因此要时刻与远程同步；
> * dev 分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
> * bug 分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
> * feature 分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。
> 总之，就是在 Git 中，分支完全可以在本地自己藏着玩，是否推送，视你的心情而定！

<!--more-->
### 抓取分支
>多人协作时，大家都会往 master 和 dev 分支上推送各自的修改。

当你从远程库 clone 时，默认情况下，你只能看到本地的 master 分支。不信可以用git branch命令看看：
`git branch`
```
* master
```
现在，你要在 dev 分支上开发，就必须创建远程 origin 的 dev 分支到本地，于是他用这个命令创建本地 dev 分支：
`git checkout -b dev origin/dev`
现在，你可以在 dev 上继续修改，然后，时不时地把 dev 分支 push 到远程：
1.`git commit -m "add ..."`
2.`git push origin dev`
```
Counting objects: 5, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 349 bytes, done.
Total 3 (delta 0), reused 0 (delta 0)
To git@github.com:michaelliao/learngit.git
   fc38031..291bea8  dev -> dev
```
>如果你对分支的修改和你的同事对分支的修改是同一个文件，如果他先push后，你再push，这时会提示冲突，需要先`git pull`把最新的提交从 origin/dev 抓下来，然后在本地合并，解决冲突，再推送。

如果git pull也失败了，可能是没有指定本地 dev 分支与远程 origin/dev 分支的链接，需要设置 dev 和 origin/dev 的链接：
`git branch --set-upstream dev origin/dev`
```
Branch dev set up to track remote branch dev from origin.
```
再`git pull`
```
Auto-merging hello.py
CONFLICT (content): Merge conflict in hello.py
Automatic merge failed; fix conflicts and then commit the result.
```
这回git pull成功，但是合并有冲突，需要手动解决，解决的方法和分支管理中的解决冲突完全一样。解决后，提交，再push：
`git commit -m "merge & fix" `
```
[dev adca45d] merge & fix hello.py
```
`git push origin dev`
```
Counting objects: 10, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (6/6), 747 bytes, done.
Total 6 (delta 0), reused 0 (delta 0)
To git@github.com:michaelliao/learngit.git
   291bea8..adca45d  dev -> dev
```
### 总结
> **因此，多人协作的工作模式通常是这样：**
>首先，可以试图用`git push origin branch-name`推送自己的修改；
>如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
>如果合并有冲突，则解决冲突，并在本地提交；
>没有冲突或者解决掉冲突后，再用`git push origin branch-name`推送就能成功！
>如果`git pull`提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream branch-name origin/branch-name`。
>这就是多人协作的工作模式，一旦熟悉了，就非常简单。
>
>---
> * 查看远程库信息，使用`git remote -v`；
> * 本地新建的分支如果不推送到远程，对其他人就是不可见的；
> * 从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用git pull抓取远程的新提交；
> * 在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；
> * 建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；
> * 从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。

上午犯困，这篇写的很懒，基本都是copy的，原文地址[多人协作](http://wiki.jikexueyuan.com/project/git-tutorial/collaboration.html)