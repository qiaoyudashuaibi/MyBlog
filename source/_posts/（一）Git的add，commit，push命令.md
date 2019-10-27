---
title: （一）Git的add，commit，push命令
date: 2019-10-27 21:05:37
tags: Git
---
今天这篇文章用来写Git的三个命令，add，commit和push命令。  

我们先来理解一下Git的工作区、暂存区和版本库。  

工作区：就是电脑中可以看的见的目录。
暂存区：英文名叫stage或index，一般存在.git目录下的index文件夹下（.git/index），所以我们把暂存区有时也叫作索引。
版本库：工作区有个隐藏的目录.git，叫做Git的版本库。  

咱们可以简单的理解，所做的工作都是在工作区完成，修改后的文件通通放入暂存区，之后通过命令将文件提交到master分支。

所以提交修改后的文件的简单流程如下：
```
    查看工作区与暂存区的差别
    git status
    将当前目录下修改的所有代码从工作区中添加到暂存区中
    git add .
    将暂存区中的内容添加到本地仓库
    git commit -m "注释"
    将远程仓库中的master中的信息同步到本地仓库master中
    git pull origin master
    将本地版本库上传到远程服务器
    git push origin master 
```

这篇文章只是简单的记录一下提交修改文件的简单流程，详细的解释会在以后的文章中出现。
