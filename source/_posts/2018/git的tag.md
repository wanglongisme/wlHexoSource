---
layout: post
title: git的tag
comments: false
categories:
  - 随笔
abbrlink: 78cec1d
date: 2018-01-08 13:55:15
tags:
 - git
---

>git里也有标签(tag)的概念，也是用于版本发布。git的标签虽然是版本库的快照，但本质还是一个指向某个commit的标识。所以，创建和删除标签都是瞬间完成的。

1.切换到需要打tag的分支
`git branch`
`git checkout master`
2.打tag
`git tag v1.0`
`git tag` 查看所有标签，<font color="B22222" >注：列出的tag，是字母顺序，不是时间顺序。</font>
<!--more-->
>打tag时，默认都是在当前分支上的最新commit上打的，如果想之前的commit上打tag，指定commit id即可。

3.指定commit上打tag
`git log --pretty=oneline --abbrev-commit` 查看commit历史记录
`git tag v0.8 4ee8404`
4.查看tag详细信息
`git show <tagname>`
5.给tag添加说明`-a`指定标签名，`-m`指定说明文字
`git tag -a v0.2 -m "this is a first tag."`
```
H:\wlHexo>git show v0.2
tag v0.2
Tagger: wanglong <wanglongisme@qq.com>
Date:   Mon Jan 8 14:14:40 2018 +0800

this is a first tag.

commit 3e10e09f11d41775e97325cc6f3eae67371da557 (HEAD -> master, tag: v0.2, tag:
 v0.1, origin/master)
Author: wanglong <wanglongisme@qq.com>
Date:   Fri Jan 5 18:43:28 2018 +0800

    source commit
...
```
6.使用私钥签名一个标签`-s`
`git tag -s v0.2 -m "use -s make a tag." 12054e3`
签名采用 PGP 签名，必须首先安装 gpg（GnuPG），如果没有找到 gpg，或者没有 gpg 密钥对，就会报错：
```
H:\wlHexo>git tag -s v0.3 -m "use -s make a tag." 12054e3
gpg: directory `/c/Users/log/.gnupg' created
gpg: new configuration file `/c/Users/log/.gnupg/gpg.conf' created
gpg: WARNING: options in `/c/Users/log/.gnupg/gpg.conf' are not yet active durin
g this run
gpg: keyring `/c/Users/log/.gnupg/secring.gpg' created
gpg: keyring `/c/Users/log/.gnupg/pubring.gpg' created
gpg: skipped "wanglong <wanglongisme@qq.com>": secret key not available
gpg: signing failed: secret key not available
error: gpg failed to sign the data
error: unable to sign the tag
```
用 PGP 签名的标签是不可伪造的，因为可以验证 PGP 签名。

### 操作标签
1.删除标签
`git tag -d v0.1`
```
H:\wlHexo>git tag -d v0.1
Deleted tag 'v0.1' (was 3e10e09)
```
>在此之前创建的标签都是本地标签，不会自动推送到远程，所以可以直接删除

2.如果要推送标签到远程，使用`git push origin <tagname>`命令:
```
H:\wlHexo>git push origin v0.2
Counting objects: 1, done.
Writing objects: 100% (1/1), 162 bytes | 162.00 KiB/s, done.
Total 1 (delta 0), reused 0 (delta 0)
To github.com:wanglongisme/wlHexoSource.git
 * [new tag]         v0.2 -> v0.2
```
这时，我的github上就出现一个v0.2的tag信息。
3.一次性推送全部尚未推送到远程的本地标签
`git push origin --tags`
4.如果要删除远程库上的标签，先删除本地，再删除远程。
`git tag -d v0.2`
`git push origin :refs/tags/v0.2`