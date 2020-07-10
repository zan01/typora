



#### Git 基本操作

> https://www.liaoxuefeng.com/wiki/896043488029600/896827951938304

1. 创建空的版本库

```
 $ git init
 Initialized empty Git repository in /test/.git/
```

添加文件到 stage(暂存区)

```
$ git add <file...>

#git add -A ：暂存所有的文件，包括新增加的、修改的和删除的文件。
#git add . ：暂存新增加的和修改的文件，不包括已删除的文件。即当前目录下所有文件。
#git add -u：暂存修改的和删除的文件，不包括新增加的文件。
```

```
$ git add readme.text
```

git commit

```
$ git commit -m" 第一次"
# 把暂存区所有文件修改提交到仓库的当前分支。
$ git commit -am ""
# 把所有已经跟踪过的文件暂存起来一并提交，从而跳过 git add 步骤
$ git commit --amend
# 重新提交，第二次提交将代替第一次提交的结果。最终只会有一个提交
```

---

提交commit 日志

退出 git log 界面 输入 q 然后回车

```
$ git log

commit e0fb004e15d025451803906a5cac8f5d9fe8ee6d

Date:   Wed Jul 17 16:42:32 2019 +0800

    第三次

commit 16695b20677c2f15676510687b732c45d6cc68bc
Author: 
Date:   Wed Jul 17 16:37:28 2019 +0800

    第二次

commit a4015dca2551a6b3a57802d3162540a1ddbbefc4
Author: 
Date:   Wed Jul 17 15:03:57 2019 +0800

     第一次
(END)
```

简化 log输入 --pretty=oneline

```
$ git log --pretty=oneline

e0fb004e15d025451803906a5cac8f5d9fe8ee6d 第三次
16695b20677c2f15676510687b732c45d6cc68bc 第二次
a4015dca2551a6b3a57802d3162540a1ddbbefc4  第一次
```

回退到上一个版本

> 上一个版本    HEAD^  上上一个版本  HEAD^^

```
git reset --hard HEAD^
```



- 工作区和暂存区

    - 工作区(本地文件夹包含 .git 就是一个本地工作区)

- 版本库（Repository）

    - 工作区中存在隐藏的. git 文件夹,其中包含了名为stage的暂存区.Git为我们自动创建的第一个分支`master`，以及指向`master`的一个指针叫`HEAD` 

        git 提交分为两步

        1. `$ git add` 添加文件(就是把文件的修改放入暂存区)
        2. `$ git commit`  把暂存区的修改提交到当前分支

---

- #### git 状态

    展示当前 git 状态 

    1. 修改的文件
    2. 新增的文件
    3. 待新增的文件
    4. 待提交的文件等

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

    