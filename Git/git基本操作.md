



#### Git 基本操作

> https://www.liaoxuefeng.com/wiki/896043488029600/896827951938304

1. 创建空的版本库

```shell
 $ git init
 Initialized empty Git repository in /test/.git/
```

**git add**

> 添加文件到 stage(暂存区)

```shell
$ git add <file...>

#git add -A ：暂存所有的文件，包括新增加的、修改的和删除的文件。
#git add . ：暂存新增加的和修改的文件，不包括已删除的文件。即当前目录下所有文件。
#git add -u：暂存修改的和删除的文件，不包括新增加的文件。
```

**git commit**

> 提交暂存区

```shell
$ git commit -m" 第一次"
# 把暂存区所有文件修改提交到仓库的当前分支。
$ git commit -am ""
# 把所有已经跟踪过的文件暂存起来一并提交，从而跳过 git add 步骤
$ git commit --amend
# 重新提交，第二次提交将代替第一次提交的结果。最终只会有一个提交
```

---

**git log**

> 日志查看

```shell
$ git log
$ git log --pretty=oneline
#简化 log输入 --pretty=oneline

```

**git reset**

> 回滚

```shell
git reset --hard HEAD^
#上一个版本    HEAD^  上上一个版本  HEAD^^
```

**git status**

```
$ git status 
```

---

- 从 HEAD 覆盖本地工作区文件的修改vi

    ```
    $git checkout -- filename
    ```

    1. 工作区做了修改未添加到暂存区(`$ git add filename`) ,撤销修改就回到和版本库一模一样的状态

- 撤销暂存区的提交

    工作区文件已经添加到暂存区 未提交,但是工作区文件又做了修改,撤销修改就回到添加到暂存区后的状态

    ```
    $ git reset HEAD <file>
    ```
    
- 查看本地库和版本库文件的区别

    ```
    $ git diff HEAD -- readme.txt 
    ```

- git 中文显示

    ```
    #不对0x80以上的字符进行quote，解决git status/commit时中文文件名乱码
    git config --global core.quotepath false
    ```

    ```
    diff
    显示工作区与暂存区的不同
    git diff
    显示暂存区与本地仓库的不同
    git diff --cached
    显示工作区，暂存区与本地仓库的不同
    git diff HEAD
    仅显示改变的文件
    git diff --name-only
    比较两次提交的差异
    git diff <commit> <commit>
    显示某次 commit 所做的更改
    git show <commit>
    ```
    
    