## 1.git是什么？

是一个分布式**版本控制**软件

## 2.git的作用是什么？

版本控制 团队协作

## 3.git的优势是什么？

分布式管理

如何下载git：百度搜索git-scm

工作区、暂存区、本地仓库、远程仓库

## git中的一些error解决方法

解决windows使用git时出现：warning: LF will be replaced by CRLF

windows中的换行符为 CRLF， 而在linux下的换行符为LF，解决办法：

`git config --global core.autocrlf false`

解决使用git status 显示中文乱码问题

`git config --global core.quotepath false`

## git命令：

#### git本地操作

**git --help**	调出帮助文档

**git +命令--help**	查看某个具体命令的帮助文档

**git init**	生成一个空的本地仓库

**git add**	将文件添加到暂存区

**git branch**	查看/新建本地分支

初次commit之前，需要配置用户邮箱及用户名，使用以下命令：

 git config --global user.email "you@example.com"
 git config --global user.name "Your Name"

**git commit** **-m "想要说的话"**		将**暂存区文件**提交到**本地仓库**

**git status**	用于查看文件状态

**git rm**	用于git文件的删除，删除本地文件，并提交暂存区

**git rm -- cache**	仅删除暂存区文件

**git checkout** 从暂存区将文件恢复到本地文件，并进行覆盖。

**git checkout 【本地分支】 【文件名】**	从所写分支拉取并覆盖文件

#### git远程操作

**git remote** 列出所有的远程仓库

**git remote add origin https://github.com/yyou124/springboot-demo.git** 从url添加远程仓库

**git push -u origin master**	向名字为origin的仓库的master的分支提交变更

**git fetch**	拉取远程仓库的变更到本地仓库

**git merge origin/master**	将远程的变更合并到本地仓库的master分支

## git文件状态

![](./git文件状态.jpg)
=======
新建文件 ---->> Untracked

使用add命令将其加入暂存区 ---->>>Staged

使用commit命令将暂存区文件提交到本地仓库 ----->>Unmodified

如果队Unmodified状态的文件进行修改====>>modified

如果队Unmodified状态的文件进行remove擦做----->Untracked

git图形化客户端-------source tree



## 什么时分支

软件项目中启动一条单独开发线的方法

1. 解决bug时新建一个分支，用于对该bug的研究

2. 可以避免版本兼容开发，避免不同版本之间的相互影响。

3. 封装一个开发阶段

### 分支命令

**git branch** 列出所有分支

**git branch 【分支命**】 创建新分支，*分支，表示当前所在分支

**git branch -d 【分支名】** 删除分支（非当前分支）

**git branch -m 【旧】 【新】** 修改分支名

**git checkout 【分支名**】 切换分支 如果modified当前分支文件后，没有commit就切换分支，会报错，因为没有commit的文件在切换分支后不会更新。

**git checkout -f 【分支名**】 强制切换分支，不会报错。慎用。

**-f 强制性参数，一定要非常小心使用，一般情况下不建议使用**。

### git日志

**git log** 用于查看git的提交历史

```c
commit e0e3fb0f8142eb668bef7a4416334e356a19ced6	//SHA-1 校验和，commit id
Author: youdeqiang <youdeqiang123@gmail.com>	//概要信息作者 邮箱
Date:   Mon Sep 24 18:01:57 2018 +0800			//提交时间
    
    git file status test	//使用commit -m选项 所输入的概要说明
```



**git log -2** 查看最近两次提交

**git log -p -2** diff两次提交

**git log --author** 查看具体某个作者的提交

**git log --oneline** 输出简要的提交信息

**git log --graph** 以一个简单的线串联起整个提交历史

### git diff命令

用来解决冲突

**git diff** **不加任何参数** 用于比较当前工作区跟暂存区的差异

**git diff --cached 或者 --staged**		用于比较工作区与本地仓库的差异

**git diff HEAD** 用于比较工作区与当前分支的差异

**git diff 【分支名】** 用于查看当前分支跟制定分支的差异

**git diff 【分支1】 【分支2】** 查看两个制定分支的差异

**git diff 【文件名】** 用于查看指定文件的差异

**git diff 【commitID】 【commitID】** 用于比较两个历史提交的差异

**git diff --stat** 用于罗列有变更的文件

```c
diff --git a/file2 b/file2		//file2的连个版本
index c200906..29e2b3c 100644
--- a/file2			//变更前的文件
+++ b/file2			//当前的文件
@@ -1 +1,2 @@ //从变更前的文件的第一行，到变更后文件地第一行往下两行有差异
 222
+111	//+表示新增一行，-表示删除一行
 
```

### reset命令
将不必要的文件从暂存区删除

更正上一次的提交，或者提交信息

版本回滚

**git reset HEAD** 【文件名】 移除暂存区文件

**git reset HEAD^**	移除最近一次提交，以及删除暂存区文件

**git reset --soft HEAD^**	移除最近移除提交，不删除暂存区文件 

​		常用于修改commit的提交信息

**git reset --soft** 将HEAD引用指向指定的提交，工作区和暂存区不会改变	

**git reset --mixed** （**default**）将HEAD引用指向指定的提交	，工作区不变和暂存区改变

**git reset --hard** 将HEAD引用指向指定的提交，工作区和暂存区都会改变（版本回滚）

### 分支合并/冲突解决

**git merge 【分支1】 【分支2】** 将分支1合并到分支2中

**git diff --name-only --diff-filter=U** 用于查看冲突文件

### 标签

**git tag 不加任何参数**，表示显示标签（以字母顺序）

**git tag 【标签名】** 默认给最近一次提交打上标签

**git tag 【标签名】【commitid】**给相应commit打上标签

**git show 【标签名】** 用于显示该标签相关的提交信息

**git tag -d 【标签名】** 删除相应的标签名

**git push 【远程分支名】【标签名】** 把某个标签（本地已经存在的，否则推送失败）推动到远程分支

#### 删除远程标签的步骤：

先删除本地标签，再删除远程标签 git push 【远程分支名】:refs/tags/标签名

标签跟commit挂钩

### 不想提交某些文件怎么办

使用**.gitignore**可以对git项目中对不必要的文件进行忽略，

一般情况下，.gitignore再项目开始创建的时候就创建，并推送到远程服务器上。这样大家再初次同步的时候，就使用到该文件，避免团队成员把无关文件传送到远程服务器上。

#### .gitignore的一些语法

*.log 表示忽略所有.log结尾的文件

123?.log 表示忽略项目中所有以123+任意字符的.log文件

/error.log 表示忽略根目录中的error.log文件

src/main/test/* 表示忽略/src/main/test目录下的所有文件

**/java/ 匹配下所有java目录下的所有文件

!/error.log 表示再之前的匹配规则下，被命中的文件，可以使用!对前面的规则进行否定

对于已经提交的远程或本地仓库的杂七杂八文件：1 先删除暂存区的文件git rm -rf --cached(递归删除)