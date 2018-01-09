---
layout: post
title: git分支
comments: false
categories:
  - 随笔
  - 2018
abbrlink: f88e729b
date: 2018-01-05 17:29:12
tags:
 - git
---

>因为git的提交是一个时间线，git分支的概念和svn也有所不同，git的分支其实是一个游标，也就是HEAD，而master是一个主分支，默认情况下HEAD是指向master的。

当新建分支时，HEAD指向新建分支，即实现了主干与分支的切换，当分支需要与主干合并时，再将master游标移动到分支所在游标处，然后将HEAD指向master，即可完成合并。
具体图片解释更形象，请参考[git分支](http://wiki.jikexueyuan.com/project/git-tutorial/create-and-merging-branches.html).

---
`git branch dev`创建分支
`git checkout dev`切换到dev分支
`git branch`列出所有分支，当前分支会有一个`*`号
`git merge dev` 合并指定分支到当前分支
```
H:\wlHexo>git merge dev
Updating e5fffd2..bd72c17
Fast-forward
 source/test.txt | 1 +
 1 file changed, 1 insertion(+)

//Fast-forward表示合并方式.
```
`git branch -d dev` 删除分支dev
<!--more-->
如果没有合并就执行删除分支的话，会提示“分支没有合并”，如果仍然想要删除的话，需要使用强制删除分支：
`git branch -D <name>` 强行删除。
---
如果master和dev都修改了同一文文件，合并时将无法执行“快速合并”，只会把各自修改的内容合并到一起，这种合并很可能冲突
> git merge dev
>Auto-merging readme.txt
>CONFLICT (content): Merge <font color=#ff0000>conflict</font> in readme.txt
>Automatic merge failed; fix conflicts and then commit the result.

这时必须先手动解决冲突后再提交，最后删除分支`git branch -d dev`
>当 Git 无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
>用git log --graph命令可以看到分支合并图。

正常合并分支时，git 会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。
如果要禁用Fast forward模式，git就会在合并时生成一个新的commit节点。这样，从分支历史上就可以看出分支信息。
禁用Fast forward合并分支：
`git merge --no--ff -m "merge with dev no--ff" dev` 这用合并方式，因为新增了commit，所以需要`-m`参数。
查看分支历史:
`git log --graph --pretty=oneline --abbrev-commit`
```
H:\wlHexo>git log --graph --pretty=oneline --abbrev-commit
*   492e850 (HEAD -> master) merge with dev no-ff
|\
| * c07a942 (dev) update test.txt
|/
* bd72c17 update test.txt
* e5fffd2 (origin/master) commit
* 12054e3 commit source folder
* 4ee8404 commit my hexo folder, exclude node_modules folder.
* a419210 delete _posts folder
* 8125357 delete assets
* 31d3fd2 rm CNAME file
* be7b4ad commit assets floder
* 63cdd8e commit _posts floder.
* c686023 commit CNAME file
```

### 分支策略<font color=#CDC5BF size=2>(极客学院上这段描述写的很好，拷贝过来，以后翻看。)</font>
在实际开发中，我们应该按照几个基本原则进行分支管理：

首先，master 分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

那在哪干活呢？干活都在 dev 分支上，也就是说，dev 分支是不稳定的，到某个时候，比如 1.0 版本发布时，再把 dev 分支合并到 master 上，在 master 分支发布 1.0 版本；

你和你的小伙伴们每个人都在 dev 分支上干活，每个人都有自己的分支，时不时地往 dev 分支上合并就可以了。

所以，团队合作的分支看起来就像这样：
![](/assets/img/2018/20180105_branch9.png)

小结
>Git 分支十分强大，在团队开发中应该充分应用。
>合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而 fast forward 合并就看不出来曾经做过合并。