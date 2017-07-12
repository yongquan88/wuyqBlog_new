---
title: git 常用命令
date: 2017-07-12 16:43:50
tags: git
---


记录一下常用的git命令

### 创建分支
``` bash
    //创建并切换到新分支
    git checkout -b branchname
    //把本地分支推送到远程
    git push origin branchname
    //查看远程分支
    git branch -r
```

### 删除分支
```
	//删除本地分支（-D 强制删除）
	git branch -D branchname
	//删除远程分支
	git push origin :branchname

```

### 打tag
```
	//本地打tag
	git tag -a v1.1 -m "注释"
	//把tag推到远程
	git push origin v1.1
	//查看所有tag
	git tag -l
```

### 删除远程tag
```
	//删除本地tag
	git tag -d v1.1
	//删除远程tag
	git push origin :v1.1
	//也可以这样
	git push origin --delete tag v1.1
```

### 远程代码库回滚
这个是重点要说的内容，过程比本地回滚要复杂
应用场景：自动部署系统发布后发现问题，需要回滚到某一个commit，再重新发布
原理：先将本地分支退回到某个commit，删除远程分支，再重新push本地分支

操作步骤如下：
```
1、 git checkout the_branch

2、 git pull

//备份一下这个分支当前的情况
3、 git branch the_branch_backup

//把the_branch本地回滚到the_commit_id
4、git reset --hard the_commit_id 

//删除远程 the_branch
5、 git push origin :the_branch

//用回滚后的本地分支重新建立远程分支
6、 git push origin the_branch

//如果前面都成功了，删除这个备份的本地分支
7、 git branch -D the_branch_backup
 
```