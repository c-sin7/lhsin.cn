---
title: 将Hexo部署到云服务器(CentOS)
author: sin
top: true
cover: true
categories: 环境配置
summary: git安装 密钥创建 建立 SSH 信任关系 nginx安装 
tags: 
  - 环境配置
  - CentOS
  - hexo
  - git
  - nginx
---

## 1. 安装git

输入下面命令即可安装

```bash
//方法一：
sudo apt install git
//方法二：
yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel perl-devel
yum install -y git
```

查看git版本

```bash
git --version 
```

## 2. 配置参数

接下来在git中配置自己的名称和电子邮件地址，可以通过使用以下命令来完成此操作：

```.vim
git config --global user.name "用户名" 
git config --global user.email "用户邮箱"
```

可以通过下面命令查看是否正确配置。

```.vim
git config --list
```

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230209171308239.png" alt="git安装与配置" style="zoom: 80%;" />

## 3.创建一个ssh key

作用：将电脑和github账号联系在一起的密钥，可以十分方便的通过git上传代码。

获取密钥的方法如下：

首先在命令行输入cd ~/.ssh，第一次配置会显示没有那个文件或目录，这是正常现象。

然后在命令行输入ssh-keygen -t rsa -C “邮箱地址”，接下来连按三次回车就可以了。

命令行代码如下：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230209171948768.png" alt="创建ssh key" style="zoom:80%;" />

密钥就创建成功了。

打开/root/.ssh文件夹下id_rsa.pub文件，复制里面的内容

## 4.登录GitHub添加ssh key

选择setting里面的SSH and GPG keys选项

![SSH and GPG keys](https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230209172417818.png)

点击New SSH keys后界面如下图所示，Title是给密钥起一个名字，随便起一个就行，之后把刚刚复制的密钥填写在下边的大框里，点击Add SSH keys即可。

![New SSH keys](https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230209172508480.png)

## 5.创建用户并配置初始化仓库

创建一个 git 仓库

```bash
useradd git 
passwd git // 设置密码
su git // 这步很重要，避免文件权限的各种问题
cd /home/git/
mkdir -p project/hexo-blog // 项目存在的真实目录,存放hexo静态文件
mkdir repos && cd repos // 放置git仓库的文件夹
git init --bare hexo-blog-repo.git// 创建一个裸露的仓库
```

![配置初始化仓库](https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230209175642145.png)

## 6.创建钩子函数

 新建文件夹hexo-blog-repo.git 在文件夹中创建钩子post-receive，把提交到 git 仓库的文件同步到 home/hexo文件夹中

```bash
cd hexo-blog-repo.git/hooks //进入hooks文件夹
vim post-receive //创建hook钩子函数文件(git提交时自动部署)，
```

![钩子函数](https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230209175759880.png)

编写内容如下：（i进入insert模式，编写完毕后按Esc，连按两次Z保存退出）

```bash
git --work-tree=/home/git/projects/hexo-blog --git-dir=/home/git/repos/hexo-blog-repo checkout -f
```

## 7.修改权限

chmod用法： 用来修改某个目录或文件的访问权限

```bash
chmod +x post-receive
exit // 退出到 root 登录
chown -R git:git /home/git/repos/hexo-blog-repo.git // 添加权限
```

## 8.测试能否拉取

在本地打开一个终端，以 ssh 的方式登录云服务器

server_ip：用户的服务器ip

```shell
ssh -v git@server_ip
// 输入密码 即可成功登录云服务器
```

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230210135945164.png" alt=" ssh 登录云服务器" style="zoom: 80%;" />

```bash
git clone git@server_ip:/home/git/repos/hexo-blog-repo.git
```

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230209180030554.png" alt="clone结果" style="zoom:80%;" />

## 9.建立客户端与服务器的 SSH 免密连接

创建 authorized_keys 以及配置权限

```bash
cd /home/git/.ssh
touch authorized_keys  //存放客户端的ssh公钥(id_rsa.pub)
chmod 600 authorized_keys   //配置权限
```
## 10.生成密钥对（已有的请忽略）

进入你本机的(windows) c:/Users/电脑名称/.ssh 文件夹下，查看是否有名为 `id_rsa.pub` 和 `id_rsa` 的文件：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230209180411071.png" alt="本机密钥对" style="zoom:67%;" />

如果有，请跳过下面 **生成密钥** 这一步：

```bash
ssh-keygen -t rsa
```

> 中途不管你提示啥，一直Enter就是了，生成成功的话会在控制台打印出一个图案

## 11.建立 SSH 信任关系（免密登录）

```bash
ssh-copy-id -i C:/Users/电脑用户名/.ssh/id_rsa.pub git@server_ip
ssh git@server_ip // 测试能否登录
```

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230209200559093.png" alt="登录情况" style="zoom: 80%;" />

注意本地 ssh-keygen生成密钥对时**最好不要对密钥对进行重命名**

## 12.限制 git 用户的权限

为了安全起见，最好是将 git 用户的权限设置为只能执行 **git clone , git push** 命令等等：

/usr/bin/git-shell

```bash
// 查看 git-shell 是否在登录方式里面
cat /etc/shells 
// 查看是否安装
which git-shell
//添加第2步显示出来的路径，通常为 /usr/bin/git-shell
vim /etc/shells
```

/etc/shells内容：

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230209201858460.png" alt="/etc/shells内容" style="zoom:80%;" />

同时修改 /etc/passwd 文件内容，更改权限：

```bash
将原来的:
git:x:1002:1002::/home/git:/bin/bash //原来的
修改为:
git:x:1001:1001::/home/git:/usr/bin/git-shell //修改之后
```

## 13.安装配置 Nginx

#### 13.1安装

```bash
cd /usr/local/src 
wget "http://nginx.org/download/nginx-1.17.8.tar.gz" //下载安装文件
tar -xvzf nginx-1.17.8.tar.gz -C ../
cd ../nginx-1.17.8
./configure --prefix=/usr/local/nginx-webServer --with-http_stub_status_module --with-http_ssl_module --with-file-aio --with-http_realip_module 
make && make install // 编译安装
alias nginx='/usr/local/nginx-webServer/sbin/nginx' //取别名为nginx，方便调用
```

根据上面的步骤，安装完成，在控制台输入

#### 13.2查看版本

```bash
nginx -v
```

可看到版本信息，代表安装成功

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230209202213615.png" alt="nginx版本" style="zoom:80%;" />

#### 13.3运行

```bash
nginx
```

如果80端口被占用

#### 13.4安装iptables服务

需要通过防火墙开放对外端口。如果服务器上没有iptables服务，需要安装。如果有，则跳过。

```bash
yum install iptables-services
systemctl mask firewalld.service
systemctl enable iptables.service
systemctl enable ip6tables.service
```

#### 13.5配置端口

进入iptables配置80端口，因为nginx默认是由80端口访问

```bash
vi /etc/sysconfig/iptables
```

打开后，默认的配置信息如下（加粗部分为新添加的）：

```bash
INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [6:696]
-A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
-A INPUT -p icmp -j ACCEPT
-A INPUT -i lo -j ACCEPT
-A INPUT -p tcp -m state --state NEW -m tcp --dport 22 -j ACCEPT

-A INPUT -p tcp -m state --state NEW -m tcp --dport 21 -j ACCEPT
-A INPUT -p tcp -m state --state NEW -m tcp --dport 80 -j ACCEPT

A INPUT -p tcp -m state --state NEW -m tcp --dport 30000:30999 -j ACCEPT
-A INPUT -j REJECT --reject-with icmp-host-prohibited
-A FORWARD -j REJECT --reject-with icmp-host-prohibited
COMMIT
```

后续需要开放其它端口，也是在此文件中添加修改即可！

修改完后，保存退出文件编辑。

```bash
:wq
```

#### 13.6重启防火墙

```bash
systemctl restart iptables.service
```

#### 13.7端口占用问题

1）**先查看80端口被什么占用了**

```bash
fuser -n tcp 80
```

2）**将占用端口杀掉**

```bash
kill -9 进程号
```

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230209203733586.png" alt="杀掉占用端口" style="zoom:80%;" />

## 14.Nginx详细配置

将 user 修改为 root //避免权限不足无法访问博客目录
将 root 解析路径修改为博客目录 /home/git/project/hexo-blog

```bash
nginx -s stop //先停止nginx
cd /usr/local/nginx-webServer/conf
vim nginx.conf //打开配置文件
nginx -s reload //重启nginx
```

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230209213256203.png" alt="Nginx原先配置" style="zoom:80%;" />

更改之后

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230209213508091.png" alt="Nginx配置更新" style="zoom:80%;" />

## 15.配置站点配置文件

config.yml 的 deploy:

```shel
deploy:
  type: git
  repo: 
        server: git@server_ip:/home/git/repos/hexo-blog-repo.git
  branch: master
```

server_ip : 即你购买的服务器的 IP 地址

部署

```bash
hexo g -d
```

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230221194613138.png" alt="image-20230221194613138" style="zoom:50%;" />

[【Nginx/Hexo】在云服务器上搭建个人博客 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/359394085)
