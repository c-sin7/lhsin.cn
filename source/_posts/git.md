---
title: git
date: 2023-02-14
author: sin
top: true
cover: true
categories: git
summary: git使用
tags: 
  - git
---

git语句：

```bash
//操作分支语句：
//初始化
git init
//添加
git add "所需提交的文件名（包括后缀）"
//提交
git commit -m "提交文件的说明信息"
//新建分支但不切换
git branch "branchName"
//新建分支并切换到新分支
git checkout -b "branchName"
//执行checkout命令切换到branchName分支
git checkout "branchName"
//合并分支
git merge "branchName"
//在branch命令指定-d选项执行，以删除分支
git branch -d "branchName"
//rebase合并
git reset --hard HEAD~

标签操作语句：
//tag命令可添加标签
git tag "tagName"
//没有使用参数而执行tag，可以显示标签列表
git tag
//在log命令添加 --decorate选项执行，可以显示包含标签资料的历史记录
git log --decorate

```

## 一、操作分支

### 1. 事先预备

新建文件夹当作git项目，此处命名gitStudy，右建点击Git Bash

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214204334201.png" alt="image-20230214204334201" style="zoom:80%;" />

在 gitStudy 文件夹中新建文本文件，此处命名test1，将其初始化并提交

具体操作：

```bash
//初始化
git init

//添加test1.txt
git add test1.txt

//提交
git commit -m "first commit"
```

效果：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214204450771.png" alt="初始化并提交" style="zoom:80%;" />

目前的历史记录：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214205149648.png" alt="image-20230214205149648" style="zoom:80%;" />

### 2. 建立分支

具体操作：

```bash
//新建分支issue1
git branch issue1

//不指定参数直接执行branch命令可以显示分支列表，前面有*的就是现在的分支
git branch
```

效果：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214203349134.png" alt="image-20230214203349134" style="zoom:80%;" />

目前的历史记录：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214205444527.png" alt="image-20230214205444527" style="zoom:80%;" />

### 3. 切换分支

在test1.txt添加新内容，此时test1.txt文件内容：

---

git是好抓手

add 把变更录入到索引中

---

具体操作：

```bash
//切换为issue1分支
git checkout issue1

//在issue1的状态下提交，历史记录会被记录到issue1分支
git add test1.txt

//在test1.txt添加add命令的说明后再提交
git commit -m "添加add操作 second commit"
```

效果：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214215138352.png" alt="image-20230214215138352" style="zoom:80%;" />

目前的历史记录：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214210607455.png" alt="image-20230214210607455" style="zoom:80%;" />

### 4. 合并分支

具体操作：

```bash
//切换为主分支
git checkout master

//合并issue1
git merge issue1
```

效果：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214215300561.png" alt="image-20230214215300561" style="zoom:80%;" />

此时test1.txt文件内容：

---

git是好抓手

add 把变更录入到索引中

---

说明：master分支指向的提交移动到和issue1同样的位置，此处是fast-forward（快进）合并。

目前的历史记录：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214211642501.png" alt="image-20230214211642501" style="zoom:80%;" />

### 5. 删除分支

具体操作：

```bash
//删除分支issue1
git branch -d issue1
```

效果：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214211917856.png" alt="image-20230214211917856" style="zoom:80%;" />

目前的历史记录：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214211928498.png" alt="image-20230214211928498" style="zoom:80%;" />

### 6. 并行操作

具体操作：

```bash
//创建issue2分支
git branch issue2

//创建issue3分支
git branch issue3

//切换到issue2分支
git checkout issue2

//查看分支
git branch
```

效果：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214212351447.png" alt="image-20230214212351447" style="zoom:80%;" />

目前的历史记录：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214212418748.png" alt="image-20230214212418748" style="zoom:80%;" />



在issue2分支的test1.txt添加新语句后提交

此时test1.txt文件内容：

---

git是好抓手

add 把变更录入到索引中

commit 记录索引的状态

---

具体操作：

```bash
//添加test1.txt
git add test1.txt

//提交
git commit -m "添加commit操作 third commit"
```

效果：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214215656043.png" alt="image-20230214215656043" style="zoom:80%;" />

目前的历史记录：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214212721879.png" alt="image-20230214212721879" style="zoom:80%;" />

在issue3分支的test1.txt添加新语句后提交添加新语句

此时test1.txt文件内容：

---

git是好抓手

add 把变更录入到索引中

pull 取得远端数据库的内容

---

具体操作：

```bash
//切换到issue3分支
git checkout issue3

//添加test1.txt
git add test1.txt

//提交
git commit -m "添加pull操作 fourth commit"
```

效果：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230215121900025.png" alt="image-20230215121900025" style="zoom:80%;" />

目前的历史记录：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214213210899.png" alt="image-20230214213210899" style="zoom:80%;" />

这样，第三次操作和第四次操作就并行进行了。

### 7. 解决合并冲突

把issue2分支和issue3分支的修改合并到master

具体操作：

```bash
//切换master分支
git checkout master

//与issue2分支合并
git merge issue2
```

效果：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214215929556.png" alt="image-20230214215929556" style="zoom:80%;" />

目前的历史记录：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214213436613.png" alt="image-20230214213436613" style="zoom:80%;" />



合并issue3分支

具体操作：

```bash
//合并issue3
git merge issue3
```

效果：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214213702756.png" alt="image-20230214213702756" style="zoom:80%;" />

此时test1.txt文件内容：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214220028270.png" alt="image-20230214220028270" style="zoom:80%;" />



在发生冲突的地方，git生成了内容的差异。

将text1.txt修改如下：

---

git是好抓手

add 把变更录入到索引中

commit 记录索引的状态

pull 取得远端数据库的内容

---

具体操作：

```bash
//重新添加
git add test1.txt

//重新提交
git commit -m "合并issue3分支 fifth commit"
```

效果：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214220448230.png" alt="image-20230214220448230" style="zoom:80%;" />

目前的历史记录：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214220531599.png" alt="image-20230214220531599" style="zoom:80%;" />

因为在这次合并中修改了冲突部分，所以会重新创建合并修改的提交记录。

这样，master的HEAD就移动到这里了。这种合并不是fast-forward合并，而是non fast-forward合并。



### 8. 用rebase合并

合并issue3分支的时候，使用rebase可以使提交的历史记录显得更简洁

现在暂时取消刚才的合并

具体操作：

```bash
//用rebase合并
git reset --hard HEAD~
```

效果：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214221128272.png" alt="image-20230214221128272" style="zoom:80%;" />

目前的历史记录：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214221143793.png" alt="image-20230214221143793" style="zoom:80%;" />

执行rebase

具体操作：

```bash
//切换到issue3分支
git checkout issue3

//对master执行rebase
git rebase master
```

效果：

和merge时的操作相同，修改在test1.txt发生冲突的部分

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214221353826.png" alt="image-20230214221353826" style="zoom:80%;" />

此时test1.txt文件内容：

在发生冲突的地方，git生成了内容的差异

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214221605562.png" alt="image-20230214221605562" style="zoom:80%;" />

和merge时的操作相同，修改在text1.txt发生冲突的部分。

---

git是好抓手

add 把变更录入到索引中

commit 记录索引的状态

pull 取得远端数据库的内容

---

rebase的时候，修改冲突后的提交不是使用commit命令，而是执行rebase命令指定 --continue选项。

若要取消rebase，指定 --abort选项

具体操作：

```bash
//添加test1.txt
git add test1.txt

//rebase，启动编辑区
git rebase --continue
```

编辑区：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230215122205553.png" alt="image-20230215122205553" style="zoom:80%;" />

效果：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230215122240171.png" alt="image-20230215122240171" style="zoom: 80%;" />

目前的历史记录：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214221938388.png" alt="image-20230214221938388" style="zoom:80%;" />

这样，在master分支的issue3分支就可以fast-forward合并。

```bash
//切换到master分支
git checkout master

//合并
git merge issue3
```

text1.txt的最终内容和merge是一样的

目前的历史记录：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214222248099.png" alt="image-20230214222248099" style="zoom:80%;" />

## 二、远端数据库操作

### 1. pull

执行pull可以取得远程数据库的历史记录

首先确认更新的本地数据库分支没有任何的更改。

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/capture_stepup3_1_1.png" alt="分支没有任何修改的情况" style="zoom:80%;" />

这时只执行fast-forward合并。图中的master是本地数据库的master分支，origin/master是远程数据库的origin的master分支。

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/capture_stepup3_1_2.png" alt="fast-forward合并" style="zoom:80%;" />

如果本地数据库的master分支有新的历史记录，就需要合并双方的修改。

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/capture_stepup3_1_3.png" alt="本地端数据库的master分支有新的历史记录" style="zoom:80%;" />

执行pull就可以进行合并。这时，如果没有冲突的修改，就会自动创建合并提交。如果发生冲突的话，要先解决冲突，再手动提交。

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/capture_stepup3_1_4.png" alt="解决冲突" style="zoom:80%;" />

### 2. fetch

执行pull，远程数据库的内容就会自动合并。

但是，有时只是想**确认本地数据库的内容而不想合并**。这种情况下，请使用fetch。

执行fetch就可以取得远程数据库的最新历史记录。取得的提交会导入到没有名字的分支，这个分支可以从名为FETCH_HEAD的退出。

例如，在本地数据库和远程数据库的origin，如果在从B进行提交的状态下执行fetch，就会形成如下图所示的历史记录。

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/capture_stepup3_2_1.png" alt="在本地端数据库和远端数据库的origin，在从B进行提交的状态下执行fetch" style="zoom:80%;" />

在这个状态下，若要把远程数据库的内容合并到本地数据库，可以合并FETCH_HEAD，或者重新执行pull。

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/capture_stepup3_2_2.png" alt="合并FETCH_HEAD" style="zoom:80%;" />

合并后，历史记录会和pull相同。实际上pull的内容是fetch + merge组成的。



### 3. push

从本地数据库push到远程数据库时，要fast-forward合并push的分支。如果发生冲突，push会被拒绝的。

若要共享在本地数据库创建的分支，需要明确的push。

因此，没有执行push就不会给远程数据库带来影响，因而可以自由的创建自己的分支。

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/capture_stepup3_3_1.png" alt="Push" style="zoom:80%;" />

基本上，远程数据库共享的提交是不能修改的。如果修改的话，跟远程数据库同步的其他数据库的历史记录会变得很奇怪的。

## 三、标签

### 1. 标签介绍

标签是为了更方便地参考提交而给它标上易懂的名称。

Git可以使用2种标签：轻标签和注解标签。

打上的标签是固定的，不能像分支那样可以移动位置。

- 轻标签
  - 添加名称
- 注解标签
  - 添加名称
  - 添加注解
  - 添加签名

一般情况下，发布标签是采用注解标签来添加注解或签名的。轻标签是为了在本地暂时使用或一次性使用。

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/capture_stepup4_1_1.png" alt="注解标签，轻标签" style="zoom:80%;" />

可以指定标签名称以退出，或reset在「修改提交」的讲解，还可以简单的恢复过去特定的状态。

### 2. 添加轻标签

具体操作：

```bash
//新建轻标签masterTag1
git tag masterTag1

//显示当前分支的标签列表
git tag

//查看显示包含标签资料的历史记录
git log --decorate
```

效果：

![image-20230215122416609](https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230215122416609.png)

### 3. 添加注解标签

git tag -a会启动编辑区：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214231023083.png" alt="image-20230214231023083" style="zoom:80%;" />

具体操作：

```bash
//添加masterTag2注解标签，启动编辑区
git tag -a masterTag2

//添加标签，指定-m选项来添加注解
git tag -am "这是masterTag3的一个注解标签" masterTag3

//显示标签的列表和注解
git tag -n
```

效果：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214231340399.png" alt="image-20230214231340399" style="zoom:80%;" />

### 4. 删除标签

具体操作：

```bash
//删除标签
git tag -d masterTag3
```

效果：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230214231722256.png" alt="image-20230214231722256" style="zoom:80%;" />

## 四、改写提交

### 1. 修改最近的提交

此时test1.txt文件内容：

---

git是好抓手

add 把变更录入到索引中

commit 记录索引的状态

pull 取得远端数据库的内容

amend 改写提交

---

启用编辑：

编辑工具会显示最近一次提交的提交消息

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230215010936094.png" alt="image-20230215010936094" style="zoom:80%;" />

把消息修改为「**amend 改写提交**」并进行保存

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230215010804119.png" alt="image-20230215010804119" style="zoom:80%;" />

现在已经修改了提交的内容，然后用log命令确认历史记录和提交消息。

具体操作：

```bash
//查看显示包含标签资料的历史记录
git log

//添加text1.txt文件
git add test1.txt

//改写提交，启动编辑区
git commit --amend

//查看显示包含标签资料的历史记录
git log
```

效果：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230215124219116.png" alt="image-20230215124219116" style="zoom:150%;" />

### 2. **改写提交**

revert

具体操作：

```bash
//用log命令确认历史记录
git log
```

效果：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230215111548289.png" alt="image-20230215111548289" style="zoom:80%;" />

此时test1.txt文件内容：

---

git是好抓手
add 把变更录入到索引中
commit 记录索引的状态
pull 取得远端数据库的内容
amend 改写提交

---

具体操作：

```bash
//用revert取消「添加pull操作 fourth commit」提交
git revert HEAD
```

启动编辑区：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230215124527527.png" alt="image-20230215124527527" style="zoom:80%;" />



编辑之后：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230215124847339.png" alt="image-20230215124847339" style="zoom:80%;" />

效果：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230215124915906.png" alt="image-20230215124915906" style="zoom:80%;" />

此时test1.txt文件内容：

---

git是好抓手
add 把变更录入到索引中
commit 记录索引的状态
amend 改写提交

---







## Git 提示Your branch is up-to-date with 'origin/master'

今天提交代码到Github的时候，提示`Your branch is up-to-date with 'origin/master'`，如下图所示：

```bash
Your branch is up to date with 'origin/master'.
Changes not staged for commit:
...
```

发现是**版本分支**的问题，按照如下步骤操作即可解决

1. 新建分支
2. 检查分支是否创建成功
3. 切换到新分支
4. 将改动提交到新分支
5. 检查是否提交成功
6. 切回主分支
7. 将新分支提交的改动合并到主分支
8. push代码到远端仓库
9. 删除新分支

具体操作：

```bash
git branch newB

git branch

git checkout newB

git add .

git commit -m "the new files"

git status

git checkout master

git merge newB

git push -u origin master

git branch -d newB
```

效果：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230215155626878.png" alt="image-20230215155626878" style="zoom:80%;" />