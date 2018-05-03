---
title: Git命令
data: 2018-04-27 21:30
tags: [Git命令]
categories: Git命令
copyright: true
---
## 切换分支
查看远程分支
``` bash
git branch -a
```

我在mxnet根目录下运行以上命令：
<!--more-->
``` bash
~/mxnet$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/master
  remotes/origin/nnvm
  remotes/origin/piiswrong-patch-1
  remotes/origin/v0.9rc1
```
可以看到，我们现在在master分支下

查看本地分支
``` bash
~/mxnet$ git branch
* master
```

切换分支
``` bash
 git checkout -b v0.9rc1 origin/v0.9rc1
Branch v0.9rc1 set up to track remote branch v0.9rc1 from origin.
Switched to a new branch 'v0.9rc1'
```


``` bash
＃已经切换到v0.9rc1分支了
$ git branch
  master
* v0.9rc1
```

＃切换回master分支
``` bash
$ git checkout master
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.
```