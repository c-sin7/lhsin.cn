---
title: nginx卸载和安装
date: 2022-02-21
author: sin
categories: 环境配置
summary: nginx卸载和安装
tags: 
  - 环境配置
  - CentOS
  - nginx
---

## nginx卸载和安装

本机环境：CentOS 7.6 ，使用yum安装的Nginx

1、查看nginx服务是否在运行。

```BASH
 ps -ef | grep nginx
```

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230221185727539.png" alt="image-20230221185727539" style="zoom:80%;" />

2、查看nginx安装目录（注意目录）

```bash
whereis nginx
```

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230221185825023.png" alt="image-20230221185825023" style="zoom:80%;" />

3、终止nginx服务运行

```bash
/usr/local/nginx-webServer/sbin/nginx -s stop
```

再次查看后，服务已经终止

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230221185908842.png" alt="image-20230221185908842" style="zoom:80%;" />

4、全局查找nginx相关的文件：

```bash
find / -name nginx*
```

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230221185937683.png" alt="image-20230221185937683" style="zoom:80%;" />

5、对相关文件（第二步骤的查询结果）进行删除

```bash
rm -rf file /usr/bin/nginx*
rm -rf file /usr/local/nginx*
```

6、使用yum卸载 nginx及相关依赖

```bash
yum remove nginx
```

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230221190125106.png" alt="image-20230221190125106" style="zoom:80%;" />

如果提示"This system is not registered with an entitlement server. You can use subscription-manager"，原因：Red Hat Subscription Manager订阅管理器，它会让你一直register。

解决：停止掉该插件的使用，在配置文件中把enable=0即可。

```bash
vim /etc/yum/pluginconf.d/subscription-manager.conf
```

<img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/image-20230221190800936.png" alt="image-20230221190800936" style="zoom:80%;" />

到此，nginx卸载删除完成。

