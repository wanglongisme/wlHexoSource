---
layout: post
title: git的远程仓库
comments: false
categories:
  - 随笔
  - 2018
date: 2018-01-05 15:21:13
tags:
 - git
---

1.配置github的ssh key.
2.github创建仓库
3.在本地目录中执行`git remote add origin git@github.com:wanglongisme/wlHexoSource.git`建立本地仓库与远程仓库的关联.添加后，远程库的名字就是origin.
`git push -u origin master`将本地库的所有内容推送到远程库
```
H:\wlHexo\source>git push -u origin master
Counting objects: 3, done.
Writing objects: 100% (3/3), 229 bytes | 229.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To github.com:wanglongisme/wlHexoSource.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```
把本地库的内容推送到远程，用`git push`命令，实际上是把当前分支 master 推送到远程。
由于远程库是空的，我们第一次推送 master 分支时，加上了`-u`参数，Git 不但会把本地的master分支内容推送的远程新的 master 分支，还会把本地的master分支和远程的master 分支关联起来，在以后的推送或者拉取时就可以简化命令。
`git push origin master` 本地做了`git commit`后,就可以把本地master分支的最新修改推送至GitHub.

删除远程仓库文件(不删除本地仓库文件)
1.`git rm -r --cached fileName`,`-r`表示递归
2.`git commit`
3.`git push origin(建立关联时,定义的库名称) master`
---

>我打算把本地hexo里的文件放到github 仓库中,这样在使用不同电脑时,download一下source目录后重新发布就可以.
>但用'git commit'时,发现有2个文件夹一直无法commit.
>原因是这两个目录中包含.git目录,应该是git识别出子目录中含有git配置,不能覆盖操作. 