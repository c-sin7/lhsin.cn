---
title: picgo图床设置与typora配置
author: Reason
date: 2023-01-11 22:19:40
top: true
cover: true
categories: 环境配置
summary: picgo图床设置与typora配置
tags: 
  - picGo
  - typora
---

# picgo图床设置与typora配置

## 前言

​	PicGo是一个热门的图床工具，是可以自动把本地图片转换成链接的一款工具，是一款简洁容易操作的图床工具，可以支持微博、腾讯云、Github、阿里云等常用图床，功能可以说非常强大。

​	Typora是一款跨平台的Markdown编辑器软件，我们常常用它来写笔记或者博客。当使用Typora做笔记时，常常需要上传知识点截图到笔记上。截图图像为本地图像（存储在自己的电脑上，当我们把电脑本地图像进行删除或者误删时，再次打开笔记之前的截图都会显示丢，或者作为博客时，需要部署到远程仓库或服务器，而本地图片显然不能满足我们的需求。

​    使用PicGo图床工具将截图图像转换成链接或者上传到远程仓库服务器，当下次打开笔记或者查看远程博客时，编辑器会通过链接返回图像，上传后删除本地图像图像也不会丢失。下面将以配置picgo来介绍图床的搭建和配置使用以及介绍typora的图床配置。    

## PicGo下载

Picgo最新图床工具下载链接：

https://github.com/Molunerfinn/PicGo

mac系统选择dmg下载，windows选择.exe下载。

![图床下载地址](https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230111200044898.png)

**此处建议下载稳定的正式版本。**

![下载最新稳定版本](https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230111200208026.png)

**翻到下面进行下载安装。**

![下载对应系统版本](https://raw.githubusercontent.com/reasonllh/IMG/main/image-20230111200504555.png)

## 图床搭建

​    下面将介绍和使用==GitHub==来作为==图床==的具体用法。由于在国内有时无法访问GitHub或者速度过慢，可以先搭个梯子。

### 搭建流程

------

1. 首先登陆 GitHub，点击右上角的==+==，点击新建一个**仓库（New repository)**。

    ![新建仓库](https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230111201103490.png)

2. 进入页面，设置仓库名称， 选择仓库类型为==公开（Public）==， 由于私有仓库只有自己能够访问，上传图像后无法显示，所以必须时公有仓库。

    ![设置远程仓库](https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230111201536456.png)

3. 创建远程仓库后，点击右上角头像，进入设置。

    ![进入设置](https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230111201701845.png)

4. 接下来需要在 github 上生成一个token以便于 PicGo  根据令牌信息上传图像到我们的仓库。进入设置后，划到最下面左边栏中选择==开发人员设置（Developer  settings）==进入页面就可以看到 Personal access tokens。

   

5. 点击==Generate new token== 创建一个新token，这里选择classic模式。

    ![Generate选项](https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230111202739291.png)

6. 生成令牌，过程如图，选择完后划到最下面按下==Generate token==，即可生成令牌。

    ![生成令牌过程](https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230111203414659.png)

7. 生成token如图所示，请注意蓝色框提醒==务必立即复制您的个人访问令牌。你将无法再看到它==，请先将生成的token复制保存下来，退出此页面后将**再也看不到该token**。

![复制令牌](https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230111203754137.png)

### PicGo配置与使用

#### 配置

------

​    打开 PicGo，进入github设置

- 仓库名格式： `用户名/仓库名`，例如`reasonllh/picgoIMG`
- 分支名：main
- token令牌：刚刚从复制保存的token令牌粘贴到此处
- 可以将此设置为默认图床

![picGo图床设置](https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230111204300355.png)

#### 使用方法

​    picgo的图片上传方式就很多了，可以将图片拖拽到此处，也可以上传图片上传，更多的用法可以参考官方文档：https://github.com/Molunerfinn/PicGo

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230210214242635.png" alt="picgo图片上传区" style="zoom:67%;" />

------

## Typora图床设置

​    相信很多小伙伴也跟Reason一样有写博客的需求，而typora是一款很多程序员使用的编写markdown格式的软件，下面将介绍typora的图床有关配置。

1. 打开`Typora`，点击左上角菜单栏进入==偏好设置==。
2. 选择 `图像` ，在`上传服务`一栏中选择`PicGo`。注意如果是windows的话还需要选择PicGo.exe的路径，最后点击`验证图片上传选项`显示成功即Typora配置图床工具完成。

![typora设置](https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230111205309304.png)

1. 将图片放入Typora笔记中，右击图像选择==上传图片==即可上传到远程仓库。

    ![上传图片选项](https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230111205714617.png)               

​                                                            
