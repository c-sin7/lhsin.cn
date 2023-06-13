一、下载安装包

  cd /usr/local/software  (software可能没有，用[mkdir](https://so.csdn.net/so/search?q=mkdir&spm=1001.2101.3001.7020)创建或者只到local目录下也行)

  [wget](https://so.csdn.net/so/search?q=wget&spm=1001.2101.3001.7020) http://nginx.org/download/nginx-1.6.2.tar.gz   (选择一个比较稳定的版本下载即可，或者手动下载后，用xshell传到该目录下也行)

 

二、解压安装

  tar -zxvf [nginx](https://so.csdn.net/so/search?q=nginx&spm=1001.2101.3001.7020)-1.6.2.tar.gz -C /usr/local   (local这个目录类似于Windows的program目录，所以一些软件可以都安装在这里)

 

三、下载依赖的库文件

  1  yum install pcre

  2  yum install pcre-devel

  3  yum install zlib

  4 yum install zlib-devel

 

四、进行configure配置

  cd /usr/local/nginx-1.6.2  && ./configure --prefix=/usr/local/nginx

![img](https://raw.githubusercontent.com/c-sin7/picgoIMG/main/20180403165135209)

五、编译安装（  cd 到解压好的nginx-1.6.2，这个目录下安装编译）

make && make install

![img](https://raw.githubusercontent.com/c-sin7/picgoIMG/main/20180403165259201)

六、启动Nginx

  执行完5步骤后，cd 到/usr/local/nginx目录下。执行ls，可以看到四个目录

 conf----配置文件 html----网页文件 logs-----日志文件 sbin------主要二进制程序

 启动命令：  /usr/local/nginx/sbin/nginx   (无参数) 启动   （-s  stop）关闭   （-s reload）重启

![img](https://raw.githubusercontent.com/c-sin7/picgoIMG/main/20180403165435137)

七、查看

查看是否成功   ps -ef | grep nginx (如果能看到两个相邻ID的进程，说明启动成功)

失败的可能    80端口被占用了。   netstat -ano | grep 80

 

如果成功的话，浏览器访问能看到欢迎页面：（http://服务器的IP:80）

![img](https://raw.githubusercontent.com/c-sin7/picgoIMG/main/20180403165545204)

 nginx的结构目录（四个conf、html、logs、sbin，其他的都是运行后生成的或者自己添加的）

![img](https://raw.githubusercontent.com/c-sin7/picgoIMG/main/20180920150536576)

 Nginx的作用都是靠着conf/nginx.conf 配置文件发挥的作用。只要能读懂它，会简单的编写，基本算是入门级别了。

![img](https://raw.githubusercontent.com/c-sin7/picgoIMG/main/20180920151421670)

[(95条消息) Centos 下 Nginx 安装、启动 、关闭、重启 教程_福尔摩千的博客-CSDN博客](https://blog.csdn.net/jrgdspuwij/article/details/104060880#:~:text=概览)

[(95条消息) CentOS7 安装nginx 无法访问的问题_李振磊的博客-CSDN博客](https://blog.csdn.net/lzl18918615216/article/details/80049471?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~Rate-1-80049471-blog-102780363.pc_relevant_vip_default&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~Rate-1-80049471-blog-102780363.pc_relevant_vip_default&utm_relevant_index=2)



##### centos下解决-bash: nginx: command not found添加环境变量：ln -s /usr/local/nginx/sbin/nginx /usr/local/bin/