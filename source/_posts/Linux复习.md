---
title: Linux复习
author: noreason
date: 2023-05-27
categories: Linux
summary: Linux复习
tags: 
  - Linux
  - 复习
---

# Linux复习

## 第一讲

### Linux的起源、历史、特点、定义

- Linux是一个类Unix内核的可以自由发布的实现版本，是一个**操作系统的底层核心（内核）**
- Linux => 内核
- Linux系统 => 内核 + 工具 + 配套软件
- 特点：

> - 开放性（遵循标准）
> - 多用户
> - 多任务
> - 良好的用户界面
> - 设备独立性（把外部设备当做文件处理）
> - 丰富的网络功能
> - 可靠的系统安全
> - 良好的可移植性

### GNU、GPL

1. GNU = GNU‘s Not Unix
2. GNU计划：1983年Richard Stallman创办GNU计划，旨在建立一套完全自由和可移植的类Unix操作系统
3. GNU GPL：GNU General Public License(GNU通用公共许可证)
4. GPL核心思想：
   保证任何人有共享、修改、发布自由软件的自由
   自由软件的衍生产品必须以GPL为重新发布的许可证
   允许公司销售自由软件（硬件/服务），提供源代码

### 常见发行版本

### 商业、共享、自由和免费软件的区别和联系

#### 商业软件

- Commercial Software
- 由开发者出售拷贝并提供技术服务
- **用户只有使用权**
- **不提供源代码**

#### 共享（试用软件）

- Shareware
- 开发者提供软件试用程序拷贝授权、升级和技术服务
- **用户在试用该程序拷贝一段时间之后，必须向开发者交纳使用费用，否则不能继续使用**
- **不提供源代码**

#### 自由软件

- Freeware或Free Software
- **源代码必须公开**
- **任何人都可以自由传播、下载、使用、改写、重新发布**
- **自由软件不一定免费**

#### 免费软件

- Freeware
- **不需付钱，但免费软件不一定提供源代码**
- **只有当自由软件免费或者免费软件提供源代码的时候才是一样的**

## 第二讲

### Linux的安装方式（区别和联系，如何选择）、安装过程、远程连接方式

### Linux内核版本号

#### 内核版本号

- **由Linus等人制定和维护，全球统一**
- 内核版本号格式：x. y. zz
- x为主版本号
- y为次版本号
- zz为次次版本号

##### 稳定版

- ​	内核的特性已经固定，代码运行稳定可靠，不再增加新的特性，要改进也只是修改代码中的错误。

##### 2.6及以下版本（x.**y**.zz）

- **次版本号=偶数 => 稳定版本**
- **次版本号=奇数 => 测试版本**

##### 3.0开始

- **次版本号**不再表示一个内核是稳定版本还是测试版本，所有发布出来的正式版本都是稳定版本

#### 发行版本号

- 由各个发行公司或者组织自行制定
- 不同公司的发行版本之间无可比性

### Linux目录结构、常见目录的作用和存放内容

- **/bin：常见系统程序目录**
- /boot：开机设定目录，也是摆放核心vmlinuz的地方
- /dev： 摆放系统设备装置文件的目录
- /etc：系统配置文件，尤其passwd，shadow
- /etc/rc.d/init.d：摆放系统开机的時候载入服务的脚本
- **/home：系统使用者的目录**
- /lib：Linux执行或编译程序函数库目录
- **/mnt：软驱与光驱接入挂载的地方**
- /proc：系统核心与执行程序的一些信息
- **/root：系统管理员的目录**
- **/usr/bin，/bin：一般执行文件摆放的地方**
- **/usr/sbin，/sbin：系统管理员常用指令集**
- /var：摆放系统日志文件的地方
- /lost+fount：摆放系统不正常产生错误时遗失的片段

### Linux系统结构图、主要组件构成

#### 系统结构图

![image-20230523100917154](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523100917154.png)

#### 主要组件构成

![image-20230523101023169](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523101023169.png)

### 关机、重启命令

**不允许普通用户关机和重启**

#### 关机

- shutdown -h now
- init 0
- halt -p
- poweroff -p

#### 重启

- shutdown -r now
- init 6
- reboot

![image-20230523102233716](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523102233716.png)

+ 例子
+ 立即关机# shutdown -h now
+ 指定10分钟后关机# shutdown -h 10
+ 在关机动作触发前取消关机动作# shutdown -c
+ 重新启动计算机# shutdown -r now

![image-20230523102338170](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523102338170.png)

+ 例子
+ 切换到图形化界面# init 5
+ 切换到多用户的字符界面# init 3

![image-20230523102421758](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523102421758.png)

+ 例子
+ 关闭系统后关闭电源# halt -p
+ 关闭系统，但不留下日记记录# halt -d

![image-20230523102504768](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523102504768.png)



### 说明文档查看

man | info

man xxx | info xxx

- 回车 下一行
- 空格 下一页
- q 退出

<img src="https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523102649602.png" alt="image-20230523102649602" style="zoom:50%;" />

## 第三讲

### Linux交互方式

![image-20230523103851661](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523103851661.png)

### shell的作用、种类、默认shell

#### 作用

- ​	Shell是一个作为**用户与Linux系统间接口的程序**，它允许用户向操作系统输入需要执行的命令，返回执行结果
- 在Linux中可存在多种Shell，**一个用户同一时刻只能使用一个shell**
- 实现自动化运维

#### 种类

- ash
  贝尔实验室开发的shell，bsh是对**ash**的**符号链接**
- bash
  GNU的Bourne Again Shell，是GNU Linux操作系统上**默认的Shell**。sh以及bash2都是对它的符号链接
- tcsh
- ksh
- zsh

#### 默认shell

- GNU Linux工具中使用的是 bash shell
- **作为/bin/sh被默认安装**
- 大多数Linux发行版中，shell程序/bin/sh实际上是对程序/bin/bash的一个链接
- 如何知道/bin/sh链接到/bin/bash？
  ls -l /bin/sh

### shell的功能（命令行提示符、自动补齐、历史记录查看、常用的快捷键、重定向、管道）

- \#

  root(超级管理员)的命令提示符

- $
  非root用户的命令提示符
  
- 命令自动补齐 

  - 输入命令/文件/目录的部分字符，按tab键
  - 列出符合前缀的匹配项列表如果唯一，则自动补齐
  - 按一下没反应，按两下

- 历史记录查看

  - 键盘↑↓键 上下翻看历史输入命令

  - ctrl + p前一条指令

  - ctrl + n后一条指令

  - ctrl + r 反向搜索命令历史记录

  	> 输入内容后，系统会找到最近一个包含这个内容的命令
  	>
  	> 找到命令后，按回车执行命令，按上下键查找该命令前后命令，按左右键移动光标并修改命令

- 光标移动

  - ctrl + a 移动光标到行首
  - ctrl + e 移动光标到行尾
  - ctrl + d 删除光标所在字符
  - ctrl + u 剪切到行首
  - ctrl + k 剪切到行尾

- 输入输出重定向(>, >>, <)

  - < 文件

  	输入重定向

  	wc -l < list.txt

  - \>文件

  	输出重定向 *覆盖原有内容*

  	ls > list.txt

  - \>\>文件

  	追加重定向 *文件末尾添加*

  	echo abc >> list.txt

- 管道(|)

  - 把前一个命令的输出作为下一个命令的输入
  - 格式：命令1 | 命令2 | 命令3 …
  - 例子：# cat /etc/passwd | grep root | wc -l

### clear、echo、ls、cd、pwd、mkdir、rmdir、rm、touch、cat、more、less、head、tail、cp、mv

#### 命令clear

作用：清空屏幕

格式： clear

#### 命令 echo

作用：打印内容

格式：echo [-n] 字符串

例子 

+ \# echo hello world

+ \# echo -n input something

#### 命令: ls

作用：显示指定工作目录下的内容

格式：ls [选项] <路径> …

| -a   | all, 列出所有文件，包含隐藏文件           |
| ---- | ----------------------------------------- |
| -l   | long, 长格式打印                          |
| -i   | inode, 列出inode节点的值                  |
| -t   | time, 按时间排序                          |
| -S   | size, 按文件大小排序                      |
| -d   | directory, 只显示目录，不显示目录下的内容 |
| -R   | recursive, 递归显示目录及子目录的内容     |

![image-20230523120450776](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523120450776.png)

例子

+ \# ls -ail
+ \# ls -lR /etc
+ \# ls -lS /var/log

#### 命令 cd

作用：切换目录

格式： cd 路径

例子

+ \# cd dir1
+ \# cd /

#### 命令 pwd

作用：显示当前路径

格式： pwd

例子# pwd

#### 命令 mkdir

作用：创建目录

格式：mkdir [选项] <目录>…

​		-p	自动创建不存在的中间目录

例子

+ \# mkdir dir1 dir2
+ \# mkdir dir1/dir3
+ \# mkdir dir4/dir5
+ \# mkdir -p dir4/dir5

#### 命令 rmdir

作用：删除目录。只能删除空目录

格式：rmdir [选项] <目录>…

​		-p	删除路径中的空目录

例子

+ \# rmdir dir1
+ \# rmdir -p dir3

#### 命令 rm

作用：删除文件或目录

格式： rm [选项] <路径>…

| -r   | 递归删除子目录的内容 |
| ---- | -------------------- |
| -f   | 强制不提示           |

例子

+ \# rm file
+ \# rm -f file
+ \# rm -r dir1
+ \# rm -rf dir1

#### 命令 touch

作用：用于改变文件的时间记录或创建一个空文件

格式：touch [选项] <文件> … 

| -a   | 改变档案的读取时间记录                 |
| ---- | -------------------------------------- |
| -m   | 改变档案的修改时间记录                 |
| -r   | 使用参考档的时间记录                   |
| -d   | 设定时间与日期，可以使用各种不同的格式 |

例子

+ \# touch file
+ \# touch -r source_file target_file

#### 命令 cp

作用：文件或目录的复制

格式：cp [选项] 原路径… 目标路径

| -a   | 复制目录时，保留链接、文件属性，并复制目录下的所有内容     |
| ---- | ---------------------------------------------------------- |
| -f   | 覆盖已存在的目标文件而不进行提示                           |
| -p   | 除复制文件的内容外，还把修改时间和访问权限也复制到新文件中 |
| -r   | 递归复制目录中的所有内容，包括子目录                       |

例子

+ cp file1 file2
+ cp file1 dir1
+ cp -r dir1 dir2

#### 命令 mv

作用：移动文件或目录(重命名)

格式： mv [选项] 原路径… 目标路径

| -i   | 目标路径如果同名，先询问是否覆盖 |
| ---- | -------------------------------- |
| -f   | 覆盖已经存在的目标文件而不给提示 |
| -n   | 不要覆盖任何已存在的文件或目录   |

例子

+ mv file1 file2

+ mv file1 dir1

+ mv dir1 dir2

#### 命令 cat

作用：连接文件并打印到标准输出设备上

格式： cat [选项] <文件> …

| -n   | 给每行编号             |
| ---- | ---------------------- |
| -b   | 除了空白行，给每行编号 |

例

+ \# cat file1 file2
+ \# cat -n file1 file2

#### 命令 more

作用：分页显示文件内容

格式： more [选项]  <文件>…

| +n   | 从第n行开始显示            |
| ---- | -------------------------- |
| -s   | 把连续的多行空行显示为一行 |

注意点：**一次性加载,只能往下翻**

基本操作

+ q：退出
+ 空格：下一页
+ 回车： 下一行

#### 命令 less

作用：分页显示文件内容

格式： less [选项] <文件>…

| -e   | 当文件显示结束后，自动退出 |
| ---- | -------------------------- |
| -f   | 强迫打开特殊文件           |
| -i   | 忽略搜索时的大小写         |
| -N   | 显示每行的行号             |
| -s   | 显示连续空行为一行         |

注意点：**支持上下翻,按需加载**

基本操作

+ q：退出
+ 空格：下一页
+ 回车： 下一行
+ 上下移动键：上下移动

#### 命令 head

作用：显示文件的开头的内容。在默认情况下显示文件的前10行内容

格式： head [选项] <文件>

| -q       | 隐藏文件名   |
| -------- | ------------ |
| -v       | 显示文件名   |
| -c<数目> | 显示的字节数 |
| -n<行数> | 显示的行数   |

例子

+ \# head file1
+ \# head -5 file1
+ \# head -n 5 file1
+ \# head -c 20 file1

#### 命令 tail

作用：显示文件的结尾的内容。在默认情况下显示文件的最后10行内容

格式： tail [选项] <文件>

| -f       | 当文件变化时输出文件新增内容 |
| -------- | ---------------------------- |
| -c<数目> | 显示的字节数                 |
| -n<行数> | 显示的行数                   |
| -v       | 显示详细的处理信息           |

例子

+ \# tail file1
+ \# tail -n 5 file1
+ \# tail -5 file1
+ \# tail -c 50 file1
+ \# tail -f file1

### 文件类型、相对路径、绝对路径、用户主目录、特殊目录、当前目录、工作目录

#### 文件类型

- 普通文件：[ - ]
  纯文字文件（ascii）或 二进制文件
- 目录： [ d ]
- 链接文件： [ l ]
- 设备文件：
  区块设备文件：[ b ];
  字符设备文件：[ c ]
- 管道文件： [ p ]
- Socket文件： [ s ]

#### 绝对路径

**指从“根”开始的路径，也称为完全路径**   # cd /usr/local/bin

#### 相对路径

**指从用户工作目录开始的路径**  # cd /usr# cd local/bin

#### 特殊目录

- **“.”代表该目录自己**
- **“..”代表该目录的父目录**
- **对于根目录，“.”和“..”都代表其自己**

#### 工作目录/当前目录

用户登录系统后，某一时刻处在的目录，也称为当前目录

#### 用户主目录

- 添加用户时为该用户建立起来的目录
- 每个用户都有自己的主目录 （普通用户一般在/home下，root用户在/root下）
- **用户主目录可以用符号 ~表示**
- 快速回到当前用户的主目录 cd ~



## 第四讲

### 用户类型

- 超级用户
  root，根用户，有最高的权限，可以对linux做任何操作
- 普通用户
  受限的权限，没有对系统的完全控制权，用户之间私人的资源是相互隔离的
- 系统用户
  与系统和程序服务相关的用户
  默认情况下，这些特殊用户的无法登录的，如果给这些用户授权登录口令后，就可以使这些用户登录系统

### /etc/passwd 作用和内容

用户信息文件

- 每一行存储一个用户的账号信息
- 用户名：加密密码：用户ID：用户组ID：用户信息：用户主目录：登录Shell
- 超级用户root的UID是0
- 系统用户的UID在1000以内
- 普通用户的UID从1000开始往上编号

### /etc/shadow /etc/group作用

#### /etc/shadow

- 口令文件
- 每一行存储一个用户的登录密码信息，加密
- 只有root用户才能读取这个文件

#### /etc/group

- 每一行记录系统中的用户组信息
- 组名：密码字段：用户组ID：用户名列表
- 用户名列表用冒号分隔多个用户名
- 默认情况下，创建用户的时候，系统会自动创建一个同名的组，作为该用户的主组。

### useradd、passwd、usermod、userdel、groupadd、groupdel、chmod、chown、chgrp、ln、tar、gzip、unzip、awk、sed、cut、tr、find、grep

#### useradd

![image-20230523125911519](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523125911519.png)

例子

+ \# useradd user1
+ \# useradd -d /home/user1024 -u 1024 -G user1 user2

#### passwd

作用：修改密码

格式：passwd  [用户名]

普通用户只能修改自己密码

root可以修改其他人

例子

+ \# passwd
+ \# passwd user1

高级应用-无交互设置密码

echo xxx | passwd --stdin root

#### usermod

![image-20230523130139601](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523130139601.png)

例子

+ \# usermod -u 2048 user2
+ \# usermod -d /home/user2048 user2

#### userdel

作用：删除用户

格式：userdel  [-r] 用户名

**root权限**

例子

+ \# userdel user2
+ \# userdel -r user1 删除与用户相关的文件和目录,如用户家目录,日志,邮箱等

#### groupadd

作用：增加用户组

格式：groupadd [-g] 组名

**root权限**

例子

+ \# groupadd user3
+ \# groupadd -g 1024 user1024  设置GID

#### groupdel

作用：删除用户组

格式：groupdel  组名

**root权限**

例子 # groupdel user3

#### chmod

![image-20230523135729391](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523135729391.png)

例子

+ \# chmod a=rwx,u-x,g-wx,o-rwx a.txt
+ \# chmod 640 a.txt
+ \# chmod -R 765 dir1

#### chown

作用：改变指定目录或文件的所属用户、所属组

格式：chown [-R] 用户名[:组名]  路径

**root权限**

例子

+ \# chown wilson a.txt
+ \# chown wilson:wilson a.txt
+ \# chown -R wilson dir1

#### chgrp

作用：改变指定目录或文件的所属组。

格式：chgrp [-R] 组名 路径

**root权限**

例子

+ \# chgrp wilson a.txt
+ \# chgrp -R wilson dir1

#### ln

![image-20230523140331387](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523140331387.png)

![image-20230523163439730](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523163439730.png)

#### tar

作用：备份文件

格式：tar [选项]  压缩文件名  路径

| -c      | 创建备份                 |
| ------- | ------------------------ |
| -C path | 切换到指定目录           |
| -f      | 指定备份文件             |
| -t      | 测试备份文件             |
| -v      | 显示指令执行过程         |
| -x      | 从备份中还原文件         |
| -z      | 通过gzip指令处理备份文件 |

例子

+ \# tar cvf dir1.tar dir1
+ \# tar xvf dir1.tar
+ \# tar xvf dir1.tar -C /tmp
+ \# tar zcvf dir1.tar.gz dir1
+ \# tar zxvf dir1.tar.gz

f必须放到最后

压缩 tar -zcvf 压缩文件名 包内文件路径

解压 tar -zxvf 压缩文件名

#### gzip

作用：用于压缩文件

格式：gzip [选项] 文件…

| -d   | 解开压缩文件           |
| ---- | ---------------------- |
| -l   | 列出压缩文件的相关信息 |
| -r   | 递归处理指定目录       |
| -v   | 显示指令执行过程       |
| -t   | 测试压缩文件是否有误   |

例子

+ \# gzip dir1
+ \# gzip -drv dir1

#### unzip

作用：用于解压缩zip文件

格式：unzip [选项] 路径

| -n     | 解压时不要覆盖原有文件 |
| ------ | ---------------------- |
| -l     | 列出压缩文件的相关信息 |
| -d dir | 指定解压时存放的目录   |
| -v     | 显示指令执行过程       |
| -t     | 测试压缩文件是否有误   |

例子

+ \# unzip a.txt.zip
+ \# unzip -d /tmp a.txt.zip

#### awk

提取列数据 用于格式化输出，将数据按照我们想要的方式来显示，并且可以做一些基本的统计工作。

![image-20230523164037934](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523164037934.png)

grep 行截取

cut（制表符分隔） awk（空格、制表符分隔） 列截取

#### sed

作用：自动编辑一个或多个文件、简化对文件的反复操作、编写转换程序等

格式：sed [选项] 处理格式路径

| a    | 在指定行号之后插入 |
| ---- | ------------------ |
| c    | 整行替换           |
| s    | 匹配替换           |
| i    | 在指定行号位置插入 |
| d    | 删除               |

<img src="https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523164526132.png" alt="image-20230523164526132" style="zoom:50%;" />

<img src="https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523164708051.png" alt="image-20230523164708051" style="zoom:50%;" />

<img src="https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523164816395.png" alt="image-20230523164816395" style="zoom:50%;" />

sed是一种几乎包括在所有UNIX平台的轻量级流编辑器。sed主要是用来将数据进行选取、替换、删除、新增的命令。

#### cut

作用：从指定文件中过滤或提取特定内容，并显示在当前屏幕上

格式：cut [选项] 路径

| -b   | 以字节为单位进行分割           |
| ---- | ------------------------------ |
| -c   | 以字符为单位进行分割           |
| -d   | 自定义分隔符，默认为制表符     |
| -f   | 与-d一起使用，指定显示哪个区域 |

例子

+ 自定义分隔符,指定显示哪个区域
	- \# cut -d: -f1,3,5 /etc/passwd
	- \# cut -d: -f 1-5 /etc/passwd
+ 以字符为单位进行分割
	- \# cut -c2-5 /etc/passwd
	- \# cut -c2,5,7 /etc/passwd

#### tr

作用：用于转换或删除文件中的字符

格式：tr [-d] 字符串1 字符串2

例子

+ \# cat /etc/passwd | tr ‘a-z’ ‘A-Z’
+ \# tr ‘a-z’ ‘A-Z’ < /etc/passwd
+ \# tr -d ‘a-c’ < test.txt

#### find

作用：查找文件或者目录

格式：find 路径 [选项] 表达式

| -amin n  | 在过去n**分钟**内被**读取**过的文件 |
| -------- | ----------------------------------- |
| -atime n | 在过去n**天**内被**读取**过的文件   |
| -cmin n  | 在过去n**分钟**内被**修改**过的文件 |
| -ctime n | 在过去n**天**内被**修改**过的文件   |
| -type c  | 文件**类型**是c的文件               |
| -perm p  | 文件**权限**为p的文件               |
| -name n  | **文件名**为n的文件                 |

例子

+ \# find . -name “\*.conf”
+ \# find / -perm 765 -name “\*.txt”
+ \# find /etc -type f -exec ls -l ‘{}’ \;
	- 查找普通格式的文件
	- 执行命令

#### grep

![image-20230523165809018](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523165809018.png)

![image-20230523170104965](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523170104965.png)

### 软连接和硬连接的区别和联系

#### 硬连接（hard link）

​	给文件一个**副本**（别名），同时建立两者之间的连接关系，修改其中一个，与其连接的文件同时被修改，如果删除其中一个，其余的文件不受影响。磁盘上只有一份数据。**硬链接是存在同一个文件系统中**。

#### 软连接(symbolic link)

​	软链接的方式则是产生一个特殊的文件，该文件的内容是指向另一个文件的位置。它只是一个**快捷方式**，删除了源文件，这个连接文件就没用了。**软链接可以跨越不同的文件系统。**

#### 区别于联系

- 适用场景
- inode节点
- 链接数
- 文件的属性
- 对链接进行操作（修改，删除）对原文件的影响
- 对原文件进行操作（修改，删除）对链接的影响
- **需要指定绝对路径，否则链接失效**

### 常见正则表达式

- ^
  锚定行的开始，如：'^grep' 匹配所有以grep开头的行
  
- \$
  锚定行的结束，如：'grep$' 匹配所有以grep结尾的行
  
- .
  匹配一个非换行符的字符，如：'gr.p' 匹配gr后接一个任意字符，然后是p
  
- *
  匹配0个或多个先前字符，如：'*grep' 匹配所有一个或多个空格后紧跟grep的行。.\*一起用代表任意字符
  
- []
  匹配一个指定范围内的字符，如：'[Gg]rep' 匹配Grep和grep
  
- [^]
  匹配一个不在指定范围内的字符，如：'[\^A-F]rep' 匹配不包含A-F的一个字母开头，紧跟rep的行
  
- \\(..\\)
  标记匹配字符，如：'\\(love\\)' ，love被标记为1
  
- \\<
  锚定单词的开始，如：'\\<grep'匹配包含以grep开头的单词的行
  
- \\>
  锚定单词的结束，如：'grep\\>'匹配包含以grep结尾的单词的行
  
- x\\{m\\}
  重复字符x，m次，如：'o\\{5\\}' 匹配包含5个o的行
  
- x\\{m,\\}
  重复字符x，至少m次，如：'o\\{5,\\}' 匹配至少有5个o的行
  
- x\\{m,n\\}
  重复字符x，至少m次，不多于n次，如：'o\\{5,10\\}'匹配5--10个o的行
  
- \w 

  匹配文字和数字字符，也就是[A-Za-z0-9]，如：'G\w*p'匹配以G后跟零个或多个文字或数字字符，然后是p

- \W 

  \w的反置形式，匹配一个或多个非单词字符，如点号句号等

- \b 

  单词锁定符，如: '\bgrep\b'只匹配grep

## 第五讲

### cal、date、wc、sort、which、whereis、su、yum、sudo

#### cal

作用：打印日期

格式：cal

| -3   | 显示最近三个月的日历   |
| ---- | ---------------------- |
| -s   | 将星期天作为月的第一天 |
| -m   | 将星期一作为月的第一天 |
| -y   | 显示当年日历           |

例子：

+ \# cal
+ \# cal -3
+ \# cal 2 2022

#### date

作用：显示或设定系统的日期与时间

格式：date [选项] 时间格式

| %H   | 小时(00..23)         |
| ---- | -------------------- |
| %M   | 分钟(00..59)         |
| %S   | 秒(00..60)           |
| %Y   | 完整月份(0000..9999) |
| %m   | 月份(01..12)         |
| %d   | 日(01..31)           |

例子

+ \# date
+ \# date ’+%Y-%m-%d %H:%M:%S’

#### wc

作用：默认统计文件内的行／字和字节数 

格式：wc  [选项] 文件路径

| -c   | 按字节统计 |
| ---- | ---------- |
| -l   | 按行数统计 |
| -m   | 按字符统计 |
| -w   | 按单词统计 |

例子

+ \# wc /etc/passwd
+ \# cat /etc/passwd | wc -l

![image-20230523171621006](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523171621006.png)

#### sort

作用：对内容排序

格式：sort [选项] 文件路径

| -f      | 排序时，将小写字母视为大写字母 |
| ------- | ------------------------------ |
| -n      | 按照数值大小排序               |
| -u      | 去重排序                       |
| -o file | 将排序后的结果存入指定的文件   |
| -r      | 以相反的顺序来排序             |

例子

+ \# sort /etc/passwd
+ \# sort -r /etc/passwd
+ \# sort -o out.txt -n /etc/passwd

sort以空格为分隔符，将一行分割为多个关键字对文件进行排序，它并没有对文件内容进行实际排序，只是将文件内容有序输出

#### which、whereis

作用：查找文件

格式： which / whereis 命令

例子

+ \# which useradd
+ \# whereis useradd
+ \# which ls
+ \# whereis ls

![image-20230523172245039](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523172245039.png)

#### su

作用：变更为其他使用者的身份。除 root 外，需要键入该使用者的密码

格式： su [选项] [用户名]

例子

+ \# su
+ \# su tak
+ \# su -c ls tak
+ \# su - tak -c ls 变更账号为tak的使用者，并执行指令（ls）后再变回原来使用者

#### yum

#### sudo

作用：以系统管理者的身份执行指令

格式： sudo 命令

CentOS7默认没有普通用户具有sudo权限

例子 \# sudo cat /etc/shadow

![image-20230523172625558](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523172625558.png)

### vi三种模式的功能、切换

命令模式

+ 启动vi后默认模式
+ 按下ESC键可进入命令模式
+ 输入的字符被当成命令，字符不回显

插入模式

+ 命令模式下通过i、a、o、c、r、s等命令进入
+ 输入的字符被当成文本内容，显示在屏幕上

末行模式

+ 命令模式下通过:、/、?等命令进入
+ 显示在屏幕的最后一行
+ 命令执行后，自动切换到命令模式

![image-20230523194304373](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523194304373.png)

### 末行模式：保存、退出、显示/取消行号、搜索、替换

![image-20230523194520961](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523194520961.png)

![image-20230523194648929](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523194648929.png)

![image-20230523194718604](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523194718604.png)

![image-20230523194821924](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523194821924.png)



### 命令模式：光标移动、删除恢复、复制粘贴、替换、切换到插入模式（含课外补充内容、课外作业）

![image-20230523194922284](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523194922284.png)

![image-20230523195049270](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523195049270.png)

![image-20230523195129791](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523195129791.png)

![image-20230523195217253](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523195217253.png)

![image-20230523195246239](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523195246239.png)

![image-20230523195347664](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523195347664.png)

![image-20230523195438758](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523195438758.png)



#### 课外补充

![image-20230523195743675](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523195743675.png)

#### 课后作业

![image-20230523195840553](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523195840553.png)

### vi与shell交互

在末行模式下用“！”符号来访问Linux的shell

- 例如
- :!cat /etc/passwd | more
- :! /bin/bash

### vi冲突处理

- 每次打开文件会创建一个名为 *.swp 的临时文件
- 当多界面编辑、vi异常退出时会导致异常
- 删除 *.swp 即可

### 文本格式转换

unix2dos（linux转window）、dos2unix（window转linux）

- 使用
- unix2dos | dos2unix filename \#格式转换后覆盖源文件
- unix2dos | dos2unix -n filename newFilename \#格式转换后存为新文件

## 第六讲

### ifconfig、ifup、ifdown、ping、netstat、service、chkconfig

#### ifconfig

![image-20230523210204529](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523210204529.png)

![image-20230523210546615](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523210546615.png)

![image-20230523210604759](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523210604759.png)



#### ifup、ifdown

![image-20230523210404221](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523210404221.png)

#### ping

作用：网络连通性测试

格式：ping [选项] <目的主机名或IP地址>

| -c <完成次数>   | 设置完成要求回应的次数 |
| --------------- | ---------------------- |
| -s <数据包大小> | 设置数据包的大小       |
| -t <存活数值>   | 设置存活数值TTL的大小  |
| -v              | 详细显示指令的执行过程 |

例子

+ \# ping www.baidu.com
+ \# ping -c 4 www.baidu.com

#### netstat

作用:用于显示网络状态

格式: netstat [选项]

| -a或--all                  | 显示所有连线中的Socket                   |
| -------------------------- | ---------------------------------------- |
| -A<网络类型>或--<网络类型> | 列出该网络类型连线中的相关地址           |
| -c或--continuous           | 持续列出网络状态                         |
| -e或--extend               | 显示网络其他相关信息                     |
| -l或--listening            | 显示监控中的服务器的Socket               |
| -n或--numeric              | 直接使用IP地址，而不通过域名服务器       |
| -p或--programs             | 显示正在使用Socket的程序识别码和程序名称 |
| -t或--tcp                  | 显示TCP传输协议的连线状况                |
| -u或--udp                  | 显示UDP传输协议的连线状况                |
| -v或--verbose              | 显示指令执行过程                         |

例子

+ \# netstat -a	（显示所有连线中的Socket）
+ \# netstat -aux  （列出所有监听UNIX端口和udp端口）
+ \# netstat -ntlp | grep port   （查看端口使用）

#### service

作用：用于对系统服务进行管理

格式：service 服务名 [ start | stop | restart | status ]

例子

+ \# service sshd restart
+ \# service atd status

#### chkconfig

作用：用于检查和设置系统的各种服务，**设置启动项**

格式：chkconfig [选项] 服务名 [状态]

| --add                 | 添加指定的新服务                                   |
| --------------------- | -------------------------------------------------- |
| --del                 | 删除指定服务                                       |
| --level<运行级别编号> | 改变服务的运行级别及启动信息                       |
| --list                | 显示所有或指定服务，以及他们在每个运行级别是否启动 |

提供了一个维护/etc/rc[0~6] d 文件夹的命令行工具，它减轻了系统直接管理这些文件夹中的符号连接的负担

chkconfig不是立即自动禁止或激活一个服务，它只是简单的改变了符号连接，需要重启才能生效

例子

+ \# chkconfig --list
+ \# chkconfig --add mysql
+ \# chkconfig --level 2345 mysql on

#### systemctl

主要负责控制systemd系统和服务管理器

是一个系统管理守护进程、工具和库的集合，用于取代System V、service和chkconfig命令

> service 对比
>
> 例子
>
> \# systemctl start network.service
>
> \# systemctl restart sshd
>
> | **daemon****命令**     | **systemctl****命令**         | **说明** |
> | ---------------------- | ----------------------------- | -------- |
> | service [服务] start   | systemctl start [unit type]   | 启动服务 |
> | service [服务] stop    | systemctl stop [unit type]    | 停止服务 |
> | service [服务] restart | systemctl restart [unit type] | 重启服务 |

> chkconfig 对比
>
> 例子
>
> \# systemctl enable nginx.service
>
> \# systemctl disable sshd
>
> | **daemon****命令**   | **systemctl****命令**         | **说明**             |
> | -------------------- | ----------------------------- | -------------------- |
> | chkconfig [服务] on  | systemctl enable [unit type]  | 设置服务开机启动     |
> | chkconfig [服务] off | systemctl disable [unit type] | 设备服务禁止开机启动 |



### 网络配置文件的各自作用、设置静态IP方法

![image-20230523211048045](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523211048045.png)

#### 设置静态IP方法

### 开机自启动三种方式

#### 开机自启动-/etc/rc.d/rc.local

1. 赋予脚本可执行权限

	\# chmod +x  /opt/script/autostart.sh

2. 在 /etc/rc.d/rc.local 末尾增加想要执行的脚本内容

	\# su - user -c '/opt/script/autostart.sh’

3.  给 /etc/rc.d/rc.local 赋予可执行权限

	\# chmod +x /etc/rc.d/rc.local

#### 开机自启动-chkconfig

1. 将脚本移动到 /etc/rc.d/init.d目录下

	\# mv  /opt/script/autostart.sh  /etc/rc.d/init.d

2. 赋予脚本可执行权限

	\# chmod +x  /etc/rc.d/init.d/autostart.sh

3. 添加脚本到开机自动启动项目中

	\# cd /etc/rc.d/init.d

	\# chkconfig --add autostart.sh

	\# chkconfig autostart.sh on

#### 开机自启动 - systemctl

默认情况下，服务通过yum install时，会自动配置好unit文件

默认在 /usr/lib/systemd/system 目录下

以Jenkins为例

\# systemctl enable jenkins.service

\# systemctl start  jenkins.service

## 第七讲

### 两个网络模式的区别与联系(含图)，如何选择

- 独立的守护进程工作模式
- 基于xinetd的工作模式

#### 独立的守护进程模式（stand-alone）

- 是Unix传统的C/S模式的访问模式
- 在Client/Server模式下，服务器监听（Listen）在一个特定的端口上等待客户连接，连接成功后服务器和客户端通过端口进行数据通信
- 守护进程的工作就是打开一个端口，并且等待（Listen）进入连接
- 如果客户端发起一个连接请求，守护进程就创建（Fork）一个子进程响应这个连接，而主进程继续监听其他的服务请求
- 运行独立的守护进程工作方式称作：stand-alone

![image-20230523230202319](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523230202319.png)

#### 基于xinetd的工作模式

- 支持对TCP、UDP、RPC服务的管理
- 可以实施基于时间段的访问控制
- 功能完备的log功能，可以记录连接成功、连接失败的行为
- 能够有效地防止拒绝服务（DoS）的攻击
- 能够限制同时运行的同一类型的服务器的数目
- 能够限制log文件大小
- 能够将某个服务绑定在特定的系统接口上，从而实现只能允许私有网络访问某项服务
- 能够实现作为其它系统的代理

![image-20230523230545547](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523230545547.png)

+ xinetd能够同时监听多个指定的端口，在接受用户请求时，它能够根据用户请求的端口不同，启动不同的网络服务进程来处理这些用户请求

+ 可以把xinetd看做一个管理启动服务的管理服务器，它决定把一个客户请求交给那个程序处理，然后启动相应的守护进程
+ 运行单个xinetd就可以同时监听所有服务端口，这样就降低了系统开销，保护系统资源
+ 但是对于访问量大、经常出现并发访问时，xinetd想要频繁启动对应的网络服务进程，反而会导致系统性能下降
+ 因此在选择基于哪种工作模式的时候，需要根据服务的使用情况具体情况具体分析

#### stand-alone与xinetd区别与联系

standalone一次性启动，运行期间一直驻留在内存中，优点是对接入信号反应快，缺点是损耗了一定的系统资源，
因此经常应用于对实时反应要求较高的 专业FTP服务器.

xinetd只在外部连接发送请求时才调用FTP进程，不适合应用在同时连接数量较多的系统。不占用系统资源。

反应速度：standalone > xinetd
占用资源：standalone > xinetd



### telnet服务的配置过程、telnet命令使用

![image-20230523231104338](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523231104338.png)

![image-20230523231152022](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523231152022.png)



### ftp两种工作模式的区别与联系(含图）

- 主动模式PORT（服务器 主动连接 客户端）
- 被动模式PASV （服务器 被动等待 客户端连接）

#### 主动模式PORT

![image-20230523231451091](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523231451091.png)

主动模式PORT(服务器 主动连接 客户端 )

指的是FTP服务器“主动”去连接客户端的数据端口来传输数据

1. 客户端从一个任意的非特权端口N（N>1024）连接到FTP服务器的命令端口（即tcp 21端口）
2. 客户端开始监听端口N+1，并发送FTP命令“port N+1”到FTP服务器
3. 服务器会从它自己的数据端口（20）“主动”连接到客户端指定的数据端口（N+1）
4. 客户端就可以和ftp服务器建立数据传输通道了

#### 被动模式PASV

![image-20230523231742421](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523231742421.png)

被动模式PASV(服务器 被动等待 客户端连接)

指的是FTP服务器“被动”等待客户端来连接自己的数据端口

1. 客户端打开两个任意的非特权本地端口（N >1024和N+1）
2. 第一个端口连接服务器的21端口，提交PASV命令
3. 服务器会开启一个任意的非特权端口（P > 1024），并发送给客户端
4. 客户端发起从本地端口N+1到服务器的端口的连接用来传送数据。（注意此模式下的FTP服务器不需要开启tcp 20端口了）

### ftp的配置过程、ftp命令的使用

#### FTP配置

![image-20230523232101620](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523232101620.png)

![image-20230523232131480](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523232131480.png)

![image-20230523232225623](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523232225623.png)

![image-20230523232258255](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523232258255.png)

![image-20230523232341046](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523232341046.png)



![image-20230523232442040](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523232442040.png)

![image-20230523232613121](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523232613121.png)

![image-20230523232715347](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523232715347.png)

![image-20230523232740672](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523232740672.png)



#### FTP命令

ftp xx.xx.xx.xx | open xx.xx.xx.xx

get | mget <filename>

put |  mput <filename>

binary | acsii 设置文件传输方式

cd 在远程主机切换目录

lcd 在本地主机切换目录

ls 在远程主机上执行ls

mkdir 在远程主机上创建目录

close 关闭

quit 退出

匿名登录

ftp | anonymous

空



## 第八讲

### shell程序的特点与用途

shell是用户和系统内核之间的接口程序

#### 特点

- shell程序可以认为是将shell命令按照控制结构组织到一个文本文件中，批量的交给shell去执行
- 不同的shell解释器使用不同的shell命令语法
- shell程序解释执行，不生成可以执行的二进制文件

#### 用途

- 可以帮助用户完成特定的任务，提高使用、维护系统的效率
- 可以更好的配置和使用Linux，实现自动化运维

### shell程序的编写、执行和调试

#### 如何执行

+ 可以使用 /bin/bash filename

+ 添加执行权限，指定路径执行
	- chmod +x /path/filename
	- ./path/filename

#### 程序编译和执行过程

一般步骤

- 编辑文件
- 保存文件
- 将文件赋予可执行的权限
- 运行及排错

常用到的命令

- vi			编辑、保存文件
- ls -l         查看文件权限
- chmod    改变程序执行权限
- 直接键入文件名运行文件

一般结构

- shell类型
- 函数
- 主过程

### 变量声明与使用、read、位置变量、$HOME、$PATH、$？

#### 变量的声明和使用

![image-20230523234011535](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523234011535.png)

![image-20230523234041505](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523234041505.png)

> 如果字符串里包含空格，就必须用引号把它们括起来
>
> 等号两边不能有空格!!!
>
> 默认情况下，所有输入的内容都是字符串



#### read

使用read将用户的输入赋值给变量

例子：

\# echo “Input something please:”

\# read something

\# echo ${something}

#### 位置变量

![image-20230523234742173](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523234742173.png)

![image-20230523234856737](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230523234856737.png)

有点类似形参与实参

$*   所有参数看做一个整体
$@ 所有参数不看做一个整体，而是区分对待

#### 环境变量（\$HOME,\$PATH,\$?）

| 环境变量 | 说明                                               |
| -------- | -------------------------------------------------- |
| $HOME    | 用户的主目录                                       |
| $IFS     | 内部的域分隔符，一般为空格符、制表符或换行符       |
| $PATH    | 寻找命令或可执行文件的搜索路径列表，路径以冒号分隔 |
| $$       | Shell脚本的进程号                                  |
| $?       | 紧邻的前驱命令的返回值 0=成功 1=失败               |
| $TERM    | 使用的终端类型                                     |
| $SHELL   | 查看当前用户所使用的的shell                        |

### 双引号、单引号和倒引号的区别和联系

#### 双引号

- 字符串通常被放在双引号中
- 如果在参数中包含一个或多个空白字符，必须给参数加双引号
- 如果把一个带有$字符的变量放在双引号中，程序执行到该行时会把变量替换为它的值
- 可用\字符取消$的特殊含义

#### 单引号

由单引号括起来的字符都作为普通字符出现

#### 倒引号

倒引号括起来的字符串都被shell解释为命令行，在执行时shell会执行该命令行，并以它的标准输出结果取代整个倒引号部分

### 简单数学运算、条件判断（字符串、数学）、逻辑运算

![image-20230524092042044](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524092042044.png)

![image-20230524092118313](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524092118313.png)



#### 条件判断

![image-20230524092757314](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524092757314.png)

| 常用字符串属性条件判断 |                                                              |
| ---------------------- | ------------------------------------------------------------ |
| string_1 = string_2    | 如果string_1和string_2两个字符串相等则返回真，否则返回假；   |
| string_1 != string_2   | 如果string_1和string_2两个字符串不相等则返回真，否则返回假； |
| -z string              | 如果字符串string的长度为0则返回真，否则返回假； zero         |
| -n string              | 如果字符串string长度不为0则返回真，否则返回假；              |
| string                 | 同-n string，如果字符串string长度不为0返回真，否则返回假。   |

| 常用的整数关系条件判断 |                                              |
| ---------------------- | -------------------------------------------- |
| mum_1 –eq num_2        | 如果num_1和num_2相等则返回真，否则返回假；   |
| mum_1 –ne num_2        | 如果num_1不等于num_2则返回真，否则返回假；   |
| mum_1 –gt num_2        | 如果num_1大于num_2则返回真，否则返回假；     |
| mum_1 –lt num_2        | 如果num_1小于num_2则返回真，否则返回假；     |
| mum_1 –le num_2        | 如果num_1小于等于num_2则返回真，否则返回假； |
| mum_1 –ge num_2        | 如果num_1大于等于num_2则返回真，否则返回假； |

#### 逻辑运算

+ 逻辑与-a：condition1 -a condition2，如果两个条件都为真，则结果为真
+ 逻辑或-o：condition1 -o condition2，如果两个条件有一个为真，则结果为真
+ 逻辑非!：! condition，结果与condition相反 

#### 例子

![image-20230524093438791](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524093438791.png)

![image-20230524093507699](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524093507699.png)

### if、casse、for、while、until

#### 控制结构

- 分支结构
- 循环结构

#### 常见分支结构

- if
- case

#### 常见循环结构

- for
- while
- until

#### if

![image-20230524093847283](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524093847283.png)

#### case

![image-20230524093920737](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524093920737.png)

![image-20230524093943991](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524093943991.png)

#### for

![image-20230524094042864](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524094042864.png)

![image-20230524094103460](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524094103460.png)

#### while/until

![image-20230524094144449](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524094144449.png)

### 要求可以 手写shell程序

#### 函数

![image-20230524094237375](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524094237375.png)

![image-20230524094550550](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524094550550.png)

![image-20230524094640412](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524094640412.png)

## 第九讲

### gcc命令使用（一次编译、分开编译、不同目录、指定头文件）

gcc：

- GNU project C and C++ compiler

- GNU Compiler Collection


GCC文件扩展名规范

+ .c为后缀的文件，是C语言源代码文件
+ .h为后缀的文件，是头文件
+ .i为后缀的文件，是已经预处理过的C源代码文件
+ .s为后缀的文件，是汇编语言源代码文件
+ .o为后缀的文件，是编译后的目标文件

基本使用格式  $ gcc  [ 选项 ]   <文件名>

| 选项                | 含义                                                         |
| ------------------- | ------------------------------------------------------------ |
| -o file             | 将经过gcc处理过的结果存为文件file，这个结果文件可能是预处理文件、汇编文件、目标文件或者最终的可执行文件。假设被处理的源文件为source.suffix，如果**这个**选项被省略了，那么生成的可执行文件**默认**名称为a.out；目标文件默认名为source.o；汇编文件默认名为source.s；生成的预处理文件则发送到标准输出设备 |
| -c                  | 仅对源文件进行编译，不链接生成可执行文件。在对源文件进行查错时，或只需产生目标文件时可以使用该选项 |
| -g[gdb]             | 在可执行文件中加入调试信息，方便进行程序的调试。如果使用中括号中的选项，表示加入gdb扩展的调试信息，方便使用gdb来进行调试 |
| -O[0、1、2、3]      | 对生成的代码使用优化，中括号中的部分为优化级别，缺省的情况为2级优化，0为不进行优化。注意，采用更高级的优化并不一定得到效率更高的代码 |
| -Dname[=definition] | 将名为name的宏定义为definition，如果中括号中的部分缺省，则宏被定义为1 |
| -**I**dir           | (大写I)在编译源程序时增加一个搜索头文件的额外目录——dir，即include增加一个搜索的额外目录 |
| -Ldir               | (大写L)在编译源文件时增加一个搜索库文件的额外目录——dir       |
| -llibrary           | (小写l)在编译链接文件时增加一个额外的库，库名为library.a     |
| -E                  | 指定GCC在生成预处理文件后停止                                |
| -S                  | 指定GCC在生成汇编文件后停止                                  |
| -w                  | 禁止所有警告                                                 |
| -Wwarning           | 允许产生warning类型的警告，warning可以是：main、unused等很多取值，最常用是-Wall，表示产生所有警告。如果warning取值为error，其含义是将所有警告作为错误（error），即出现警告就停止编译。 |

#### 一步编译、分步编译

![image-20230524100017488](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524100017488.png)

![image-20230524100042597](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524100042597.png)

#### 不同目录、指定头文件

![image-20230524100829869](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524100829869.png)

![image-20230524101038353](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524101038353.png)

### make工具

#### 作用：

根据makefile文件中预定的规则完成对特定文件的编译，最后生成对应的可执行文件

#### 原理：

判断依赖项是否为最新，否则生成新的目标

![image-20230524101302717](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524101302717.png)

### make层次图、makefile文件

#### make层次图

![image-20230524101831820](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524101831820.png)

#### makefile文件

![image-20230524101542449](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524101542449.png)



### gdb调试工具的基本使用

| file  | **指定需要进行调试的程序**                       |
| ----- | ------------------------------------------------ |
| step  | **单步（行）执行，如果遇到函数会进入函数内部**   |
| next  | **单步（行）执行，如果遇到函数不会进入函数内部** |
| run   | **启动被执行的程序**                             |
| quit  | **退出****gdb****调试环境**                      |
| print | **查看变量或者表达式的值**                       |
| break | **设置断点，程序执行到断点就会暂停起来**         |
| shell | **执行其后的****shell****命令**                  |
| list  | **查看指定文件或者函数的源代码，并标出行号**     |

### 静态函数库、动态函数库的创建与使用

+ 静态函数库 名字一般是libxxx.a
+ 动态函数库 名字一般是libxxx.so 
+ 相对于静态函数库，动态函数库在编译的时候并没有被编译进目标代码中，程序执行到相关函数时才调用该函数库里的相应函数，因此动态函数库所产生的可执行文件比较小
+ 使用GCC编译器可以将函数库与自己开发的程序链接起来例如libc.so中包含了标准的输入输出函数，当链接程序进行目标代码链接时会自动搜索该程序并将其链接到可执行文件中

#### 静态函数库的创建与使用

![image-20230524102735534](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524102735534.png)

![image-20230524102748878](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524102748878.png)

![image-20230524102822392](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524102822392.png)

![image-20230524102835779](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524102835779.png)

#### 动态函数库的创建与使用

![image-20230524103518948](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524103518948.png)

![image-20230524103541573](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524103541573.png)

## 第十讲

### 磁盘设备的命名方式

Linux系统磁盘设备命名方式遵循一定的规则

- 前两个字母表示分区所在设备的类型
  hd：IDE硬盘
  sd：SCSI硬盘（U盘，移动硬盘等）
- 第三个字母表示分区在哪个设备上
  hda：第一块IDE硬盘
  sda：第一块SCSI硬盘
  sdb：第二块SCSI硬盘
- 数字表示分区的次序
  hda1：第一块IDE硬盘第一个分区
  sdb2：第二块SCSI硬盘第二个分区
- 查看硬盘及分区情况
  fdisk -l

### Linux的文件系统、VFS的功能和作用（含图）

#### 常见的文件系统

FAT、NTFS、ExtFAT、ext2、ext3、xfs、APFS

#### Linux支持哪些文件系统

输入命令 cat /proc/filesystems 查看

#### 虚拟文件系统VFS

VFS并不是一个实际的文件系统。只存在于内存，系统启动时建立，系统关闭时消亡

##### 功能

- 记录可用文件系统的类型
- 将设备与对应的文件系统联系起来
- 处理面向文件的通用操作
- 涉及到针对文件系统的操作时，把他们映射到相关的物理文件系统

##### 作用

- 更好的支持多种不同的文件系统，把文件系统从操作系统和系统服务中分离处理来，在它们之间使用了一个接口层，也就是虚拟文件系统VFS（Virtual File System）
- VFS是Linux内核中的软件层，它在内核中提供了一组标准的、抽象的文件操作，允许不同的文件系统实现共存，并向用户空间程序提供统一的文件系统接口
- 通过VFS将不同的文件系统的实现细节隐藏起来，从外部看上去，所有的文件系统都是一样的

![image-20230524104104803](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524104104803.png)

### 设备挂载过程

- 查看设备：使用命令 “fdisk -l” 可以查看系统的存储设备
- 挂载设备：首先使用mkdir命令建立挂载点目录，然后再使用mount命令挂载相关设备
- 访问设备
- 卸载设备：用户在使用完挂载设备后，不能直接将挂载设备从系统拔出，否则会出现问题，严重的会导致系统崩溃。系统必须先执行卸载命令然后再把该设备拔出

### mkfs、fdisk、mount、umount、df、du、whoami、who、w、jobs、bg、fg、&（后台进程启动）

#### mkfs

作用：把指定的设备格式为指定的文件系统

格式：mkfs [选项][-t <文件系统类型>] [设备名称] [区块数]

例子# mkfs –t ext3 /dev/hda4

#### fdisk

作用：创建和维护分区表

格式：fdisk [必要参数][选择参数]

| -l   | 列出素所有分区表           |
| ---- | -------------------------- |
| -u   | 与-l配合使用，显示分区数目 |

例子

+ \# fdisk -l
+ \# fdisk -lu

#### mount

作用：挂载Linux系统外的文件

格式：mount [选项] <挂载设备名称>  <挂载点>

| -t                 | 指定文件系统类型，通常不必指定。mount 会自动选择正确的类型  |
| ------------------ | ----------------------------------------------------------- |
| -o auto、-o noauto | 打开/关闭自动挂上模式                                       |
| -o defaults        | 使用预设的选项 rw, suid, dev, exec, auto, nouser, and async |
| -o ro              | 用只读模式挂上                                              |
| -o rw              | 用可读写模式挂上                                            |

例子：

+ \# mount  -t  ext2  /dev/fd0  /mnt/floppy
+ \# mount  -o  iocharset=cp936 /dev/sda1  /mnt/usb
+ \# mount  -o ro /dev/hda1 /mnt

#### umount

作用：卸除文件系统

格式：umount [选项] 挂载点或设备名

| -a                | 卸除/etc/mtab中记录的所有文件系统                  |
| ----------------- | -------------------------------------------------- |
| -n                | 卸除时不要将信息存入/etc/mtab文件中                |
| -r                | 若无法成功卸除，则尝试以只读的方式重新挂入文件系统 |
| -t <文件系统类型> | 仅卸除选项中所指定的文件系统                       |
| -v                | 执行时显示详细的信息                               |

例子

+ \# umount /mnt/cd
+ \# umount -v /dev/sda1

#### df

作用：查看磁盘空间使用情况

格式：df [选项] [路径]

| -a   | --all 包含所有的具有 0 Blocks 的文件系统     |
| ---- | -------------------------------------------- |
| -h   | --human-readable 使用人类可读的格式          |
| -i   | --inodes 列出 inode 资讯，不列出已使用 block |
| -l   | --local 限制列出的文件结构                   |
| -t   | --type=TYPE 限制列出文件系统的 TYPE          |
| -T   | --print-type 显示文件系统的形式              |

例子

+ \# df 
+ \# df -ahT

#### du

作用：统计目录或文件所占磁盘空间大小

格式：du [选项/参数] [目录名…]

| -a   | 递归显示制定目录中各个文件及下级目录中各文件占用的数据块数 |
| ---- | ---------------------------------------------------------- |
| -h   | 以友好直观方式显示信息，即以KB或MB为单位                   |
| -b   | 以字节为单位列出磁盘空间使用情况                           |
| -m   | 以MB为单位显示                                             |
| -s   | 对每个目录参数只给出占用的数据块总数                       |

例子	du -m /tmp

#### whoami/who/w

whoami	查看当前登录用户名称

id	查看当前登录用户信息[-u] 只显示UID[-g] 只显示GID

who	查看当前登录用户列表[-H] 显示标题[-l] 显示来源

w	查看当前登录用户情况，who的增强版

![image-20230524110919905](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524110919905.png)

#### jobs、bg、fg、&

![image-20230524111235420](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524111235420.png)

![image-20230524111328669](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524111328669.png)

### 进程的概念、进程和程序的区别与联系

#### 进程的概念

- Linux系统上所有运行的东西都可以称之为一个进程，如每个用户任务、每个系统管理任务
- 进程是一个程序的运行

Linux操作系统包括三种不同类型的进程

- 交互进程：由shell启动的进程
- 批处理进程：这种进程和终端没有联系，是一个进程序列
- 守护进程：在后台持续运行的进程

#### 进程和程序的区别与联系

- 程序只是一个静态的指令集合，不占系统的运行资源，只占用磁盘空间
- 进程是一个随时都可能发生变化的、动态的、使用系统运行资源（cpu，内存等）的程序
- 一个程序可以启动多个进程



### at和crontab的区别与联系、各自的创建、删除、查看

#### at和crontab的区别与联系

- at命令产生的进程调度不具有周期性，只能在时间条件满足时执行一次（不具有周期性）
- crontab让使用者在固定时间或固定时间间隔执行程序（重复周期性）

#### at

作用：指定在将来的某个时间点执行某些命令

用法： at [选项] [时间]

| -m            | 当 at 工作完成后，无论命令是否输出，都用 E-mail 通知执行 at 命令的用户。 |
| ------------- | ------------------------------------------------------------ |
| -c 工作标识号 | 显示该 at 工作的实际内容。                                   |
| -t 时间       | 在指定时间提交工作并执行，时间格式为 [[CC]YY]MMDDhhmm。      |
| -d            | 删除某个工作，需要提供相应的工作标识号（ID），同 atrm 命令的作用相同。 |
| -l            | 列出当前所有等待运行的工作，和 atq 命令具有相同的额作用。    |
| -f 脚本文件   | 指定所要提交的脚本文件。                                     |

| HH:MM                      | 比如 04:00 AM。如果时间已过，则它会在第二天的同一时间执行    |
| -------------------------- | ------------------------------------------------------------ |
| Midnight(midnight)         | 代表 12:00 AM（也就是 00:00）                                |
| Noon(noon)                 | 代表 12:00 PM（相当于 12:00）                                |
| Teatime(teatime)           | 代表 4:00 PM（相当于 16:00）                                 |
| 英文月名 日期 年份         | 比如 January 15 2018 表示 2018 年 1 月 15 号，年份可有可无   |
| MMDDYY、MM/DD/YY、MM.DD.YY | 比如 011518 表示 2018 年 1 月 15 号                          |
| now+时间                   | 以 minutes、hours、days 或 weeks 为单位，例如 now+5 days 表示命令在 5 天之后的此时此刻执行 |

##### 交互式

在shell提示符下输入”at 时间”，然后按回车键。这时在下一行shell会等待用户继续输入要执行的命令。每一行输入一个命令，所有命令都输入完毕后按Ctrl+d键结束

##### 指定文件

将各个命令写入shell脚本中，然后使用下面格式设置在指定时间执行shell脚本中的命令

at 时间 -f 脚本文件

例子

+ at -l | atq 任务号
+ at -d | atrm 任务号
+ at -c 任务号

#### crontab

+ at命令产生的进程调度不具有周期性，只能在时间条件满足时执行一次

+ 但很多时候需要重复地周期性地执行某个程序

+ crontab用来让使用者在固定时间或固定时间间隔执行程序
+ cron命令在系统启动时由一个shell脚本自动启动，进入后台，crond守护进程(/etc/init.d/crond)
+ cron启动后搜索/var/spool/cron目录，寻找以/etc/passwd文件中的用户名命名的crontab文件，被找到的这种文件将载入内存
+ 如果没有crontab文件，就转入“休眠”状态，释放系统资源
+ cron每分钟“醒”过来一次，查看当前是否有需要运行的命令
+ 如果发现某个用户设置了crontab文件，它将以该用户的身份去运行文件中指定的命令。命令执行结束后，任何输出都将作为邮件发送给crontab的所有者，或者/etc/crontab文件中MAILTO环境变量中指定的用户。
+ 对用户来说，只需要关注自己的crontab文件的撰写，不需干涉crond进程的执行
+ 因为一个用户只有一个crontab文件，所以，crontab文件不能直接创建或者直接修改(root可以)，必须通过crontab命令得到
+ crontab命令用于安装、删除或者列出用于驱动cron后台进程的crontab文件

![image-20230524120928953](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524120928953.png)

![image-20230524121029254](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524121029254.png)

![image-20230524121115822](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524121115822.png)

每隔1分钟打印当前时间

\*/1 0-23/1 \* \* \* date

### ps、kill、free

#### ps

作用:显示当前进程的状态

格式：ps [选项]

| -A   | 列出所有的进程               |
| ---- | ---------------------------- |
| -w   | 显示加宽可以显示较多的资讯   |
| -au  | 显示较详细的资讯             |
| -aux | 显示所有包含其他使用者的行程 |
| -e   | 显示所有进程                 |
| -f   | 采用全格式显示               |

例子

+ \# ps -ef | grep sshd
+ \# ps -aux | grep vsftpd

![image-20230524121641123](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524121641123.png)

#### kill

作用:删除执行中的程序或工作

格式： kill \[-s <信息名称或编号>][程序]	 kill \[-l <信息编号>]

| 1 (HUP)   | 重新加载进程     |
| --------- | ---------------- |
| 9 (KILL)  | 杀死一个进程     |
| 15 (TERM) | 正常停止一个进程 |

例子

+ \# kill -9 pid
+ \# kill -HUP pid
+ \# kill -l

> 解除系统死锁，内存回收
>
> Linux 的 kill 命令是向进程发送信号，kill 不是杀死的意思，-9 表示无条件退出，但由进程自行决定是否退出，这就是为什么 kill -9 终止不了系统进程和守护进程的原因
>
> killall命令
>
> \# killall -KILL atd		#按进程名

#### free

作用：显示内存状态，包括实体内存，虚拟的交换文件内存，共享内存区段，以及系统核心使用的缓冲区等

格式：free \[选项]

| -b           | 以Byte为单位显示内存使用情况               |
| ------------ | ------------------------------------------ |
| -k           | 以KB为单位显示内存使用情况                 |
| -m           | 以MB为单位显示内存使用情况                 |
| -h           | 以合适的单位显示内存使用情况，最大为三位数 |
| -o           | 不显示缓冲区调节列                         |
| -s<间隔描述> | 持续观察内存使用状况                       |
| -t           | 显示内存总和列                             |

例子	# free -mt

### 日志文件

- 日志文件（log files）是包含关于系统消息的文件，包括内核、服务、在系统上运行的应用程序等
- 多数的日志文件位于/var/log目录下，不同的日志文件记载不同的信息
- 某些程序（如apache）在/var/log中有单独的日志文件目录
- 多数日志文件都是用纯文本格式，可以使用任何文本编辑器如vi查看它们
- 大多数日志文件都需要拥有特权才允许查看



## 第十一讲

### Docker与虚拟机的区别

Docker 是一个应用打包、分发、部署的工具。

Docker：可理解为一个轻量的虚拟机，它只虚拟你软件需要的运行环境，多余的一点都不要。

普通虚拟机：一个完整而庞大的系统，包含各种不管你要不要的软件。

| **特性** | **普通虚拟机**                                               | **Docker**                                           |
| -------- | ------------------------------------------------------------ | ---------------------------------------------------- |
| 跨平台   | 通常只能在桌面级系统运行，例如 Windows/Mac，无法在不带图形界面的服务器上运行 | 支持的系统非常多，各类 Windows 和 Linux 都支持       |
| 性能     | 性能损耗大，内存占用高，因为是把整个完整系统都虚拟出来了     | 性能好，只虚拟软件所需运行环境，最大化减少没用的配置 |
| 自动化   | 需要手动安装所有东西                                         | 一个命令就可以自动部署好所需环境                     |
| 一致性   | 环境一致性不高，不同系统差异大                               | 一致性好，不同系统都一样部署方式                     |

### Docker的优势

![image-20230524123222121](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524123222121.png)

### docker search, pull, images, run, start, stop, restart, ps, rm, attach, exec, commit, build, tag, push

#### docker search

![image-20230524123336236](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524123336236.png)

#### pull

![image-20230524123408198](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524123408198.png)

#### images

![image-20230524123450342](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524123450342.png)

![image-20230524123606248](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524123606248.png)

#### run,start

![image-20230524123657006](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524123657006.png)

![image-20230524123803620](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524123803620.png)

![image-20230524123909818](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524123909818.png)

![image-20230524124010881](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524124010881.png)

#### ps,stop,restart

![image-20230524124225263](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524124225263.png)

![image-20230524124243556](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524124243556.png)

#### rm

![image-20230524124346500](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524124346500.png)

#### attach,exec

![image-20230524124452193](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524124452193.png)

#### commit,build

![image-20230524124623789](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524124623789.png)



![image-20230524124714327](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524124714327.png)

![image-20230524124757327](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524124757327.png)

### Dockerfile

![image-20230524141658951](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524141658951.png)

| FROM [镜像]                            | 指定新镜像所基于的镜像，第一条指令必须为FROM指令，每创建一个镜像就需要一条FROM指令，例如centos:7。from有两层含义：①开启一个新的镜像②必须写的一行指令 |
| -------------------------------------- | ------------------------------------------------------------ |
| MAINTAINER [名字]                      | 说明新镜像的维护人信息（可写可不写）                         |
| RUN命令                                | 每一条RUN后面跟一条命令，在所基于的镜像上执行命令，并提交到新的镜像中，RUN必须大写 |
| CMD [“要运行的程序”，“参数1”、“参数2”] | 指定启动容器时需要运行的命令或者脚本，Dockerfile只能有一条CMD命令，如果指定多条则只能执行最后一条，“bin/bash”也是一条CMD,并且会**覆盖**image镜像里面的cmd。 |
| EXPOSE [端口号]                        | 指定新镜像加载到Docker时要开启的端口暴露端口，就是这个容器暴露出去的端口号。 |
| ENV [环境变量] [变量值]                | 设置一个环境变量的值，会被后面的RUN使用。容器可以根据自己的需求创建时传入环境变量，镜像不可以。 |
| ADD [源文件/目录] [目标文件/目录]      | ①将源文件复制到目标文件，源文件要与Dockerfile位于相同目录中，②或者是一个URL，③若源文件是压缩包则会将其解压缩。 |
| COPY [源文件/目录] [目标文件/目录]     | 将本地主机上的文件/目录复制到目标地点，源文件/目录要与Dockerfile在相同的目录中，copy只能用于复制，add复制的同时，如果复制的对象是压缩包，ADD还可以解压，copy比add节省资源。 |
| **VOLUME [“****目录****”]**            | 在容器中创建一个挂载点，简单来说就是-v，指定镜像的目录挂载到宿主机上（**由容器创建和管理**）。 |
| USER [用户名/UID]                      | 指定运行容器时的用户                                         |
| WORKDIR [路径]                         | 为后续的RUN、CMD、ENTRYPOINT指定工作目录，相当于是一个临时的“cd"，否则需要使用绝对路径，例如workdir /opt。移动到opt目录，并在这下面的指令都是在opt下执行。 |

![image-20230524142247004](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524142247004.png)



## 第十二讲

### X  Window的作用和组成（含图）、每个组成部分的作用

#### X Window

>  一种以位图方式显示的软件窗口系统
>
> 诞生于1984，比Microsoft Windows要早
>
> 是一套独立于内核的软件
>
> X Window系统由三个基本元素组成
>
> X 服务端
>
> X 客户端
>
> X通信通道

- X Server
- X Client
- Xlib

![image-20230524142918786](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524142918786.png)

#### X Server (X服务端)

>  是控制输入及输出设备并维护相关资源的程序，它接收输入设备的信息，并将其传给X Client，而将X Client传来的信息输出到屏幕上(在屏幕上构造方块(窗口)，然后画出里面的元素)
>
> 每一套显示设备只对应唯一的X Server
>
> 由系统供应商提供，通常无法被用户修改
>
> 只是一个普通的用户程序 

#### X Client(X客户端)

> 是应用程序的核心部分，它与硬件无关，每个应用程序就是一个X Client
>
> X Client可以是终端仿真器(Xterm)或图形界面程序，它不直接对显示器绘制或者操作图形，而是与X Server通信，由X Server控制显示
>
> X Client无法直接影响视窗行为或显示效果，它们只能发送一个请求给X Server，由X Server来完成这些的请求 
>
> 多种多样的X Client程序向X Server发出请求，由X Server运算得出结果，再显示到指定的地方去

#### X通信通道

> X通信通道的主体是xlib（X函数库）
>
> X Client调用xlib，利用相应的通信功能向X Server发出请求 
>
> X Server完成任务之后，同样调用xlib把结果显示指点的设备上去

#### X Window的特点 

+ 良好的网络支持

	X Window采用了C/S网络结构，X Client和X Server可以通过网络来通信，而且有良好的网络透明性

+ 个性化的窗口界面

	X Window并未对窗口界面作统一的规范，程序员可以根据需求自行设计，其中最有名的就是后面将要介绍的GNOME与KDE

+ 不内嵌于操作系统

	X Window只定义了一个标准，而不属于某个操作系统，因此可在不同的操作系统上运行相同的X Window软件

### 修改系统运行级别（含运行级别0 3  5 6）

![image-20230524143809829](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524143809829.png)

![image-20230524143854798](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230524143854798.png)



## 实验

1、2

4、5、6、7

## 题型

- 选择题      20题，每题1分，20分
- 简答题        6题，每题5分，30分
- 编码题        3题，6\*1 + 7\*2分，20分
- 综合应用题 3题，每题10分，30分

## 易错

