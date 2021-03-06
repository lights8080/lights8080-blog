---
title: Git学习笔记
categories:
  - 技术
tags:
  - Git
abbrlink: a91eaa72
date: 2021-07-08 00:00:00
---

Git

<!-- more -->

https://codewords.recurse.com/issues/two/git-from-the-inside-out
这篇文章解释了 Git 是如何工作的。它假设您对 Git 足够了解，可以使用它来对您的项目进行版本控制。

https://blog.csdn.net/qq_32452623/article/details/78905181
Git三大特色之WorkFlow(工作流)

https://nvie.com/posts/a-successful-git-branching-model/
A successful Git branching model


## 分支管理
![](https://gitee.com/lights8080/lights8080-oss/raw/master/2021/07/unknown.jpg)
Production 分支
也就是我们经常使用的Master分支，这个分支最近发布到生产环境的代码，最近发布的Release， 这个分支只能从其他分支合并，不能在这个分支直接修改

Develop 分支
这个分支是我们是我们的主开发分支，包含所有要发布到下一个Release的代码，这个主要合并与其他分支，比如Feature分支

Feature 分支
这个分支主要是用来开发一个新的功能，一旦开发完成，我们合并回Develop分支进入下一个Release

Release分支
当你需要一个发布一个新Release的时候，我们基于Develop分支创建一个Release分支，完成Release后，我们合并到Master和Develop分支

Hotfix分支
当我们在Production发现新的Bug时候，我们需要创建一个Hotfix, 完成Hotfix后，我们合并回Master和Develop分支，所以Hotfix的改动会进入下一个Release

## 工作区（Working Directory）

![](https://gitee.com/lights8080/lights8080-oss/raw/master/2021/07/DFS0Z5.png)

git add命令实际上是把文件添加到Stage
git commit就是往master分支上提交更改


## 常用命令
![](https://gitee.com/lights8080/lights8080-oss/raw/master/2021/07/RJ7iyg.png)

```sh
git revert：撤销某次操作，此次操作之前和之后的commit和history都会保留，并且把这次撤销
git clean：删除工作目录中所有没有tracked过的文件
git reset：返回到某个节点
git clone：命令用于从远程主机克隆一个版本库。Git支持https和ssh协议，https每次需要输入密码速度慢
git pull：命令用于取回远程主机某个分支的更新，与本地的指定分支合并
git push：命令用于将本地分支的更新，推送到远程主机
git remote：远程仓库管理
git fetch：命令用于将远程主机版本库中更新内容取回本地，可指定分支
git log：显示提交历史
git merge：合并分支


###（分支管理）
#基于远程分支“master”，创建本地分支dev
$git checkout -b dev origin/master
#创建分支并切换。相当于执行git branch dev和git checkout dev两条命令
$git checkout -b dev
#切换到master分支
$git checkout master

git reset：返回到某个节点
#（默认方式）回退到某个版本，只保留源码，取消了commit ，取消了add
$git reset --mixed HASH
#回到当前分支最新的版本，不保留修改（不可逆）
$git reset --hard [HASH]
#返回到某个节点。回退了commit的信息，保留修改
$git reset --soft HASH
#从add中返回到之前的状态，保留修改
$git reset -q 文件


#列出Git配置
$git config --list
#设置用户名
$git config --global user.name "Jerry Mouse"
#设置邮箱ID
$git config --global user.email "jerry@yiibai.com"
(如果省略--global选项，那么配置是具体当前的Git存储库)

git stash    #储藏当前工作现场，等以后恢复现场继续工作
git stash list    #查询保存的工作现场列表
git stash apply stash@{0}    #恢复指定的stash

# -----

# 强行拉取远程分支覆盖本地
$git reset --hard origin/master
# 把本地的dev 分支强制推送到远端 master
git push origin dev:master -f

```