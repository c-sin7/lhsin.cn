---
title: CentOS下安装yum
author: sin
date: 2023-02-09
top: true
cover: true
categories: 环境配置
summary: CentOS下安装yum
tags: 
  - 环境配置
  - CentOS
  - yum
---

# CentOS下安装yum

查看已安装的yumrpm -qa|grep yum

删除已有的yumrpm -aq|grep yum|xargs rpm -e --nodeps

下载以下安装包wget http://tel.mirrors.163.com/centos/7/os/x86_64/Packages/pyth

## 1.查看已安装的yum

```vim
rpm -qa|grep yum
```

## 2.删除已有的yum

```vim
rpm -aq|grep yum|xargs rpm -e --nodeps 
```

## 3.下载所需安装包

```vim
wget http://tel.mirrors.163.com/centos/7/os/x86_64/Packages/python-2.7.5-89.el7.x86_64.rpm 
wget http://tel.mirrors.163.com/centos/7/os/x86_64/Packages/python-iniparse-0.4-9.el7.noarch.rpm 
wget http://tel.mirrors.163.com/centos/7/os/x86_64/Packages/yum-3.4.3-168.el7.centos.noarch.rpm
wget http://tel.mirrors.163.com/centos/7/os/x86_64/Packages/yum-metadata-parser-1.1.4-10.el7.x86_64.rpm
wget http://tel.mirrors.163.com/centos/7/os/x86_64/Packages/yum-plugin-fastestmirror-1.1.31-54.el7_8.noarch.rpm
```

如果找不到以上版本，可以到 [http://tel.mirrors.163.com/centos/7/os/x86_64/Packages/](http://tel.mirrors.163.com/centos/7/os/x86_64/Packages/?login=from_csdn) 下载最新版本

![下载最新版本](https://raw.githubusercontent.com/c-sin7/picgoIMG/main/20210505211959838.png)

## 4.安装

```vim
rpm -ivh python-2.7.5-89.el7.x86_64.rpm python-iniparse-0.4-9.el7.noarch.rpm --nodeps --force
rpm -ivh yum-metadata-parser-1.1.4-10.el7.x86_64.rpm --nodeps --force
rpm -ivh yum-3.4.3-168.el7.centos.noarch.rpm yum-plugin-fastestmirror-1.1.31-54.el7_8.noarch.rpm --nodeps --force
```

## 5.更改 yum源

- 到该网站 [http://mirrors.163.com/.help/centos.html](http://mirrors.163.com/.help/centos.html?login=from_csdn) 下载配置文件，重命名为CentOS-Base.repo

  - 首先备份/etc/yum.repos.d/CentOS-Base.repo

    ```vim
    mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
    ```

  - 下载对应版本repo文件， 放入/etc/yum.repos.d/（操作前请做好相应备份）

    [CentOS7](http://mirrors.163.com/.help/CentOS7-Base-163.repo?login=from_csdn)

    [CentOS6](http://mirrors.163.com/.help/CentOS6-Base-163.repo?login=from_csdn)

    [CentOS5](http://mirrors.163.com/.help/CentOS5-Base-163.repo?login=from_csdn)

  - 运行以下命令生成缓存

  ```vim
  yum clean all
  yum makecache
  ```

- 修改配置文件

  - 运行一下命令打开CentOS-Base.repo文件

  ```vim
  cd /etc/yum.repos.d 
  
  vim CentOS-Base.repo
  ```

  > 也可以通过Xftp7软件编辑，更加方便快捷

  - 将以下配置更换Centos-Base.repo里的内容

  ```vim
  # CentOS-Base.repo
  #
  # The mirror system uses the connecting IP address of the client and the
  # update status of each mirror to pick mirrors that are updated to and
  # geographically close to the client.  You should use this for CentOS updates
  # unless you are manually picking other mirrors.
  #
  # If the mirrorlist= does not work for you, as a fall back you can try the
  # remarked out baseurl= line instead.
  #
  #
   
  [base]
  name=CentOS-$releasever - Base
  #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os
  baseurl=https://mirrors.ustc.edu.cn/centos/$releasever/os/$basearch/
  gpgcheck=1
  gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
   
  #released updates
  [updates]
  name=CentOS-$releasever - Updates
  # mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates
  baseurl=https://mirrors.ustc.edu.cn/centos/$releasever/updates/$basearch/
  gpgcheck=1
  gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
   
  #additional packages that may be useful
  [extras]
  name=CentOS-$releasever - Extras
  # mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras
  baseurl=https://mirrors.ustc.edu.cn/centos/$releasever/extras/$basearch/
  gpgcheck=1
  gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
   
  #additional packages that extend functionality of existing packages
  [centosplus]
  name=CentOS-$releasever - Plus
  # mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus
  baseurl=https://mirrors.ustc.edu.cn/centos/$releasever/centosplus/$basearch/
  gpgcheck=1
  enabled=0
  gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
  ```

  - 配置完成后更新缓存

  ```vim
  yum clean all
  yum makecache
  ```

完成以上步骤就可以成功在Linux安装上yum