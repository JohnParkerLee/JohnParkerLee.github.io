---
title: Git基本操作(待更新)
date: 2020-08-19 19:06:21
tags: git
categories: Git
---
## 常用命令

对于[learninggitbranch](https://learngitbranching.js.org/?locale=zh_CN)学习材料的总结。

 ### Git Branch

```bash
# 先创建新分支，再进行切换
git branch <branch_name>
git checkout <branch_name>

# 创建新分支，同时切换到新创建的分支
git checkout -b <branch_name>


# 强制修改分支指向的位置，由<branch_name1>-><branch_name2>~[num]
git branch -f <branch_name1> <branch_name2>~[num]
```

### Git Merge

当我们在新建的分支上完成开发任务后，开发完成需要合并回主线。

假设当前位于master分支，需要合并bugFix分支

```bash
git merge bugFix
```



### Git Rebase

对提交的记录进行复制。

假设位于bugFix分支，需要合并到master分支

```bash
git rebase master
git checkout master
git rebase bugFix
```



### Git Head

1. Head的指向

```bash
# 查看HEAD的指向
cat .git/HEAD

# 若HEAD指向一个引用，可以使用如下方法查看指向
git symbolic-ref HEAD

# 将HEAD指向于<branch_name>的前一个位置
git checkout <branch_name>^

# 将HEAD指向于<branch_name>的第前[num]的位置
git checkout <branch_name>~[num]
```

2. 分离的Head

   分离的Head指的是直接让HEAD指向具体的某个提交记录，而不是分支名，可以通过***git log***获取对应提交记录的哈希值。

```bash
# 假设当前HEAD为HEAD -> master -> C0(hash value)
git checkout C0
# 修改后的指向为HEAD -> C0
```



Git 
