---
layout: post
title: git如何使用bug分支
comments: false
categories:
  - 随笔
abbrlink: 518e617c
date: 2018-01-08 10:24:22
tags:
 - git
---

>在实际开发中，可能会遇到这种情况，正在一个分支中开发某功能，正开发到一半，突然要去修复一个紧急的bug。这时可以使用git的stash。
>git提供了一个`stash`功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作。

<!--more-->
1.实际操作前，先`git status`看下状态，发现有文件修改。
```
H:\wlHexo>git status
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        deleted:    "source/_posts/2018/git\345\205\245\351\227\250.md"
        modified:   "source/_posts/2018/git\345\221\275\344\227\250.md"
        modified:   "source/_posts/2018/git\347\232\204\350\345\272\223.md"
        deleted:    source/test.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .deploy_git/
        .npmignore
        node_modules/
        public/
        "source/_posts/2018/git\345\246\202\344\275\225\345\210\206\346\224\257.md"

no changes added to commit (use "git add" and/or "git commit -a")
```
2.执行`git stash`
```
H:\wlHexo>git stash
Saved working directory and index state WIP on master: 3e10e09 source commit
```
3.再次`git status`，注意最后一行“nothing added to commit”。
```
H:\wlHexo>git status
On branch master
Your branch is up to date with 'origin/master'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .deploy_git/
        .npmignore
        node_modules/
        public/
        "source/_posts/2018/git\345\246\202\344\275\345\210\206\346\224\257.md"

nothing added to commit but untracked files present (use "git add" to track)
```
4.然后就可以在master主分支上创建修改bug分支，修改完bug后，与主干合并即可。
5.修复完bug后，切回开发的功能分支 branch checkout xxx。
6.这时需要从工作现场恢复分支
7.首先`git stash list`查看工作现场信息(因为我是在master上操作的，所以显示master，实际中应该为分支名称)
```
H:\wlHexo>git stash list
stash@{0}: WIP on master: 3e10e09 source commit
```
8.第一种恢复方式是用`git stash apply`恢复，但是恢复后，stash 内容并不删除，你需要用`git stash drop`来删除；
9.另一种方式是用`git stash pop` 恢复的同时把 stash 内容也删了：
```
H:\wlHexo>git stash pop
Removing source/test.txt
Removing source/_posts/2018/git入门.md

Warning: Your console font probably doesn't support Unicode. If you experience s
trange characters in the output, consider switching to a TrueType font such as C
onsolas!
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        deleted:    "source/_posts/2018/git\345\205\245\351\227\250.md"
        modified:   "source/_posts/2018/git\345\221\275\344\273\244\345\205\245\351\227\250.md"
        modified:   "source/_posts/2018/git\347\232\204\350\277\234\347\250\213\272\223.md"
        deleted:    source/test.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .deploy_git/
        .npmignore
        node_modules/
        public/
        "source/_posts/2018/git\345\246\202\344\275\225\344\275\277\224\257.md"

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (ede53222c8d0b545479d626ca0b6c0f193544f81)
```
可以发现git状态又回到之前了，最后一行显示删除工作现场，这时再用`git stash list`查看，就没有工作现场信息了。

10.如果存在多个stash，可以使用`git stash apply stash@{0}`指定从某个现场恢复

---
总结
>修复 bug 时，我们会通过创建新的 bug 分支进行修复，然后合并，最后删除；
>当手头工作没有完成时，先把工作现场`git stash`一下，然后去修复 bug，修复后，再`git stash pop`，回到工作现场。