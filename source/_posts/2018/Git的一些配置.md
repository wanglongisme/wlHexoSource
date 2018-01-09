---
layout: post
title: Git的一些配置
comments: false
categories:
  - 随笔
abbrlink: fb0a70bd
date: 2018-01-08 14:52:32
tags:
 - git
---

>实际开发过程中，一些文件是不需要提交的，但每次`git status`又显示出来，还要人工的去筛选很不方便，所以可以使用git的配置文件忽略某些文件和目录.

1.在git的工作区中创建`.gitignore`文件.
2.文件内写入需要忽略的文件:
```
#my configurations
.deploy_git/
.npmignore
node_modules/
```
<!--more-->
>哪些文件需要忽略?
> * 编译后产生文件，如java的class文件等
> * 含有敏感信息文件，密码文件等
> * 自动生成的文件或中间文件等，如某些IDE工作空间的.project文件

`.gitignore`文件需要提交版本库，并做版本管理，像管理其他文件一样。

### Git颜色
Git 显示颜色，`git config --global color.ui true` 
//没执行这命令前，我的git一直也有颜色，执行后也没什么变化，没深入研究。
### Git命令缩写
>有些命令比较长，单词也不好记，git提供了简写方式，方便执行。

* `git config --global alias.st status` 执行后，就可以使用`git st`代替`git status`
* 配置一个`git last`，让其显示最后一次提交信息：`git config --global alias.last 'log -1'`
* 配置 Git 的时候，加上`--global`是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用。

------
1.仓库的 Git 配置文件都放在.git/config文件
```
[core]
	repositoryformatversion = 0
	filemode = false
	bare = false
	logallrefupdates = true
	symlinks = false
	ignorecase = true
[remote "origin"]
	url = git@github.com:wanglongisme/wlHexoSource.git
	fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
	remote = origin
	merge = refs/heads/master
[alias]
	last = 'log'
```
//alias下就是缩写的配置.
2.当前用户的 Git 配置文件放在用户主目录下的一个隐藏文件.gitconfig中
我的文件在 C:\Users\log\\.gitconfig
```
[user]
	email = wanglongisme@qq.com
	name = wanglong
[color]
	ui = true
[alias]
	last = 'log'
```
>遇到一个小坑
>我用`git config --global alias.last 'log -1'`配置后，执行命令报错
```
H:\wlHexo>git last
fatal: Bad alias.last string: unclosed quote
```
>查看文件发现last = 'log 少了半边单引号，不知道什么原因，只能手动修改配置文件或使用双引号。


### 关于log的缩写
* `git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"`
然后执行`git lg`输出:
```
H:\wlHexo>git lg
* 3e10e09 - (HEAD -> master, tag: v0.2, origin/master) source commit (3 days ago) <wanglong>
* ce799b2 - rm --cached source (3 days ago) <wanglong>
* e465250 - update blog markdown files. (3 days ago) <wanglong>
* 221e42f - update test.txt (3 days ago) <wanglong>
* 445ac92 - update test.txt (3 days ago) <wanglong>
* 2eeab07 - Create README.md (3 days ago) <wanglongisme>
* e5fffd2 - commit (3 days ago) <wanglong>
* 12054e3 - commit source folder (3 days ago) <wanglong>
* 4ee8404 - commit my hexo folder, exclude node_modules folder. (3 days ago) <wanglong>
* a419210 - delete _posts folder (3 days ago) <wanglong>
* 8125357 - delete assets (3 days ago) <wanglong>
* 31d3fd2 - rm CNAME file (3 days ago) <wanglong>
* be7b4ad - commit assets floder (3 days ago) <wanglong>
* 63cdd8e - commit _posts floder. (3 days ago) <wanglong>
* c686023 - commit CNAME file (3 days ago) <wanglong>
```
* `git config --global alias.lg1 "log --pretty=oneline --abbrev-commit"`
执行`git lg1`输出
```
H:\wlHexo>git lg1
3e10e09 (HEAD -> master, tag: v0.2, origin/master) source commit
ce799b2 rm --cached source
e465250 update blog markdown files.
221e42f update test.txt
445ac92 update test.txt
2eeab07 Create README.md
e5fffd2 commit
12054e3 commit source folder
4ee8404 commit my hexo folder, exclude node_modules folder.
a419210 delete _posts folder
8125357 delete assets
31d3fd2 rm CNAME file
be7b4ad commit assets floder
63cdd8e commit _posts floder.
c686023 commit CNAME file
```


