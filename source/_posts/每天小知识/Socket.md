---
title: Socket
author: sin
categories: 小知识
summary: 
tags: 
  - Socket
---

# Socket

**TCP/IP、UDP**

1. TCP/IP（Transmission Control Protocol/Internet Protocol）即传输控制协议/网间协议，是一个工业标准的协议集，它是为广域网（WANs）设计的。

2. UDP（User Data Protocol，用户数据报协议）是与TCP相对应的协议。它是属于TCP/IP协议族中的一种。

   <img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/20190718154523875.png" style="zoom:80%;" />

   **Socket是什么呢？**
       Socket是应用层与TCP/IP协议族通信的中间软件抽象层，它是一组接口。

   在设计模式中，Socket其实就是一个门面模式，它把复杂的TCP/IP协议族隐藏在Socket接口后面，对用户来说，一组简单的接口就是全部，让Socket去组织数据，以符合指定的协议。

   <img src="https://raw.githubusercontent.com/c-sin7/picgoIMG/main/20190718154556909.png" alt="img"  />

   先从服务器端说起。

   服务器端先初始化Socket，然后与端口绑定(bind)，对端口进行监听(listen)，调用accept阻塞，等待客户端连接。

   在这时如果有个客户端初始化一个Socket，然后连接服务器(connect)

   如果连接成功，这时客户端与服务器端的连接就建立了。

   客户端发送数据请求，服务器端接收请求并处理请求，然后把回应数据发送给客户端，客户端读取数据，最后关闭连接，一次交互结束。

   # 1、网络中进程之间如何通信？

   本地的进程间通信（IPC）有很多种方式，但可以总结为下面4类：

   - 消息传递（管道、FIFO、消息队列）
   - 同步（互斥量、条件变量、读写锁、文件和写记录锁、信号量）
   - 共享内存（匿名的和具名的）
   - 远程过程调用（Solaris门和Sun RPC）

   本地可以通过进程PID来唯一标识一个进程，但是在网络中这是行不通的。

   其实TCP/IP协议族已经帮我们解决了这个问题，网络层的“**ip地址**”可以唯一标识网络中的主机，而传输层的“**协议+端口**”可以唯一标识主机中的应用程序（进程）。

   利用三元组（ip地址，协议，端口）就可以标识网络的进程了。

   # 2、socket的基本操作

   socket是“open—write/read—close”模式的一种实现，socket提供了这些操作对应的函数接口。下面以TCP为例，介绍几个基本的socket接口函数。

   ## 2.1、socket()函数

   ```vim
   int socket(int domain, int type, int protocol);
   ```

   socket函数对应于普通文件的打开操作。普通文件的打开操作返回一个文件描述字

   而**socket()**用于创建一个socket描述符（**socket descriptor**），它唯一标识一个socket。

   这个socket描述字跟文件描述字一样，后续的操作都有用到它，把它作为参数，通过它来进行一些读写操作。

   正如可以给fopen的传入不同参数值，以打开不同的文件。创建socket的时候，也可以指定不同的参数创建不同的socket描述符，socket函数的三个参数分别为：

   - **domain**：即**协议域**，又称为协议族（family）。

     常用的协议族有，AF_INET、AF_INET6、AF_LOCAL（或称AF_UNIX，Unix域socket）、AF_ROUTE等等。

     协议族决定了socket的地址类型，在通信中必须采用对应的地址，如AF_INET决定了要用ipv4地址（32位的）与端口号（16位的）的组合、AF_UNIX决定了要用一个绝对路径名作为地址。

   - **type**：指定socket**类型**。

     常用的socket类型有，SOCK_STREAM、SOCK_DGRAM、SOCK_RAW、SOCK_PACKET、SOCK_SEQPACKET等等。

   - **protocol**：故名思意，就是**指定协议**。

     常用的协议有，IPPROTO_TCP、IPPTOTO_UDP、IPPROTO_SCTP、IPPROTO_TIPC等，它们分别对应TCP传输协议、UDP传输协议、STCP传输协议、TIPC传输协议

   注意：并不是上面的type和protocol可以随意组合的，如SOCK_STREAM不可以跟IPPROTO_UDP组合。当protocol为0时，会自动选择type类型对应的默认协议。

   当我们调用**socket**创建一个socket时，返回的socket描述字它存在于协议族（address family，AF_XXX）空间中，但没有一个具体的地址。如果想要给它赋值一个地址，就必须调用bind()函数，否则就当调用connect()、listen()时系统会自动随机分配一个端口。

   ## 2.2、bind()函数

   正如上面所说bind()函数把一个地址族中的特定地址赋给socket。

   例如对应AF_INET、AF_INET6就是把一个ipv4或ipv6地址和端口号组合赋给socket。

   ```vim
   int bind(int sockfd, const struct sockaddr *addr, socklen_t addrlen);
   ```

   函数的三个参数分别为：

   - sockfd：即socket描述字，它是通过socket()函数创建，唯一标识一个socket。**bind()函数就是将给这个描述字绑定一个名字**

   - addr：一个const struct sockaddr *指针，指向要绑定给sockfd的协议地址。这个地址结构根据地址创建socket时的地址协议族的不同而不同，如ipv4对应的是：

     ```c++
     struct sockaddr_in {
         sa_family_t    sin_family; 
         in_port_t      sin_port;   
         struct in_addr sin_addr;   
     };
     
     
     struct in_addr {
         uint32_t       s_addr;     
     };
     ```

     ipv6对应的是：

     ```c++
     struct sockaddr_in6 { 
         sa_family_t     sin6_family;    
         in_port_t       sin6_port;      
         uint32_t        sin6_flowinfo;  
         struct in6_addr sin6_addr;      
         uint32_t        sin6_scope_id;  
     };
     
     struct in6_addr { 
         unsigned char   s6_addr[16];    
     };
     ```

     Unix域对应的是：

     ```c++
     #define UNIX_PATH_MAX    108
     
     struct sockaddr_un { 
         sa_family_t sun_family;                
         char        sun_path[UNIX_PATH_MAX];   
     };
     ```

   通常服务器在启动的时候都会绑定一个众所周知的地址（如ip地址+端口号），用于提供服务，客户就可以通过它来接连服务器；

   而客户端就不用指定，有系统自动分配一个端口号和自身的ip地址组合。

   这就是为什么通常服务器端在listen之前会调用bind()，而客户端就不会调用，而是在connect()时由系统随机生成一个。

   

   ### 网络字节序与主机字节序

   **主机字节序**

   就是我们平常说的大端和小端模式：不同的CPU有不同的字节序类型，这些字节序是指整数在内存中保存的顺序，这个叫做主机序。

   　　a) Little-Endian就是低位字节排放在内存的低地址端，高位字节排放在内存的高地址端。高高低低——小端

   　　b) Big-Endian就是高位字节排放在内存的低地址端，低位字节排放在内存的高地址端。

   **网络字节序**：

   4个字节的32 bit值以下面的次序传输：首先是0～7bit，其次8～15bit，然后16～23bit，最后是24~31bit。

   即大端字节序。**由于TCP/IP首部中所有的二进制整数在网络中传输时都要求以这种次序，因此它又称作网络字节序。**

   字节序，顾名思义字节的顺序，就是大于一个字节类型的数据在内存中的存放顺序，一个字节的数据没有顺序的问题了。

   

   所以： 在将一个地址绑定到socket的时候，请**先将主机字节序转换成为网络字节序**，将其转化为网络字节序再赋给socket。

   ## 2.3、listen()、connect()函数

   如果作为一个服务器，在调用socket()、bind()之后就会调用listen()来监听这个socket

   如果客户端这时调用connect()发出连接请求，服务器端就会接收到这个请求。

   ```c++
   int listen(int sockfd, int backlog);
   int connect(int sockfd, const struct sockaddr *addr, socklen_t addrlen);
   ```

   listen函数的第一个参数即为要监听的socket描述字，第二个参数为相应socket可以排队的**最大连接个数**。socket()函数创建的socket默认是一个主动类型的，listen函数将socket变为**被动类型的，等待客户的连接请求**。

   connect函数的第一个参数即为客户端的socket描述字，第二参数为服务器的socket地址，第三个参数为socket地址的长度。客户端通过调用connect函数来建立与TCP服务器的连接。

   ## 2.4、accept()函数

   TCP服务器端依次调用socket()、bind()、listen()之后，就会监听指定的socket地址了。

   TCP客户端依次调用socket()、connect()之后就想TCP服务器发送了一个连接请求。

   TCP服务器监听到这个请求之后，就会调用accept()函数取接收请求，这样连接就建立好了。

   之后就可以开始网络I/O操作了，即类同于普通文件的读写I/O操作。

   ```c++
   int accept(int sockfd, struct sockaddr *addr, socklen_t *addrlen);
   ```

   accept函数的第一个参数为服务器的socket描述字，第二个参数为指向struct sockaddr *的指针，用于返回客户端的协议地址，第三个参数为协议地址的长度。

   如果accpet成功，那么其返回值是**由内核自动生成的一个全新的描述字**，代表与返回客户的TCP连接。

   注意：accept的第一个参数为服务器的socket描述字，是服务器开始调用socket()函数生成的，称为**监听socket描述字**；而accept函数返回的是已连接的socket描述字。一个服务器通常通常仅仅只创建一个监听socket描述字，**它在该服务器的生命周期内一直存在**。内核为每个由服务器进程接受的客户连接创建了一个已连接socket描述字，当服务器完成了对某个客户的服务，相应的已连接socket描述字就被关闭。

   ## 2.5、read()、write()等函数

   至此服务器与客户已经建立好连接了。可以调用网络I/O进行读写操作了，即实现了网咯中不同进程之间的通信。

   网络I/O操作有下面几组：

   - read()/write()
   - recv()/send()
   - readv()/writev()
   - recvmsg()/sendmsg()
   - recvfrom()/sendto()

   推荐使用recvmsg()/sendmsg()函数，这两个函数是最通用的I/O函数

   实际上可以把上面的其它函数都替换成这两个函数。它们的声明如下：

   ```c++
   #include 
   
   ssize_t read(int fd, void *buf, size_t count);
   ssize_t write(int fd, const void *buf, size_t count);
   
   #include 
   #include 
   
   ssize_t send(int sockfd, const void *buf, size_t len, int flags);
   ssize_t recv(int sockfd, void *buf, size_t len, int flags);
   
   ssize_t sendto(int sockfd, const void *buf, size_t len, int flags,
                         const struct sockaddr *dest_addr, socklen_t addrlen);
   ssize_t recvfrom(int sockfd, void *buf, size_t len, int flags,
                           struct sockaddr *src_addr, socklen_t *addrlen);
   
   ssize_t sendmsg(int sockfd, const struct msghdr *msg, int flags);
   ssize_t recvmsg(int sockfd, struct msghdr *msg, int flags);
   ```

   read函数是负责从fd中读取内容。

   ​	当读成功时，read返回实际所读的字节数，如果返回的值是0表示已经读到文件的结束了，小于0表示出现了错误。

   ​	如果错误为EINTR说明读是由中断引起的，如果是ECONNREST表示网络连接出了问题。

   write函数将buf中的nbytes字节内容写入文件描述符fd。

   ​	成功时返回写的字节数。失败时返回-1，并设置errno变量。

   在网络程序中，当我们向套接字文件描述符写时有俩种可能。

   ​	1)write的返回值大于0，表示写了部分或者是 全部的数据。

   ​	2)返回的值小于0，此时出现了错误。

   ​	如果错误为EINTR表示在写的时候出现了中断错误。如果为EPIPE表示 网络连接出现了问题(对方已经关闭了连接)。

   ## 2.6、close()函数

   完成了读写操作就要关闭相应的socket描述字，好比操作完打开的文件要调用fclose关闭打开的文件。

   ```c++
   #include 
   int close(int fd);
   ```

   close一个TCP socket的缺省行为时把该socket标记为已关闭，然后立即返回到调用进程。该描述字不能再由调用进程使用，也就是说不能再作为read或write的第一个参数。

   注意：close操作只是使相应socket描述字的引用计数-1，只有当引用计数为0的时候，才会触发TCP客户端向服务器发送终止连接请求。

   # 3、socket中TCP的三次握手建立连接详解

   tcp建立连接要进行“三次握手”，即交换三个分组。大致流程如下：

   - 客户端向服务器发送一个SYN J
   - 服务器向客户端响应一个SYN K，并对SYN J进行确认ACK J+1
   - 客户端再想服务器发一个确认ACK K+1

   只有就完了三次握手，但是这个三次握手发生在socket的那几个函数中呢？请看下图：

   [![image](https://raw.githubusercontent.com/c-sin7/picgoIMG/main/aHR0cHM6Ly9pbWFnZXMuY25ibG9ncy5jb20vY25ibG9nc19jb20vc2t5bmV0LzIwMTAxMi8yMDEwMTIxMjIxNTc0NzYyODYucG5n)](http://images.cnblogs.com/cnblogs_com/skynet/201012/201012122157467258.png)

   socket中发送的TCP三次握手

   - 当客户端调用connect时，触发了连接请求，向服务器发送了SYN J包，这时connect进入阻塞状态；
   - 服务器监听到连接请求，即收到SYN J包，调用accept函数接收请求向客户端发送SYN K ，ACK J+1，这时accept进入阻塞状态；
   - 客户端收到服务器的SYN K ，ACK J+1之后，这时connect返回，并对SYN K进行确认；
   - 服务器收到ACK K+1时，accept返回，至此三次握手完毕，连接建立。

   # 4、socket中TCP的四次握手释放连接详解

   上面介绍了socket中TCP的三次握手建立过程，及其涉及的socket函数。

   现在介绍socket中的四次握手释放连接的过程

   [![image](https://raw.githubusercontent.com/c-sin7/picgoIMG/main/aHR0cHM6Ly9pbWFnZXMuY25ibG9ncy5jb20vY25ibG9nc19jb20vc2t5bmV0LzIwMTAxMi8yMDEwMTIxMjIxNTc0OTQ2OTMucG5n)](http://images.cnblogs.com/cnblogs_com/skynet/201012/201012122157487616.png)

   socket中发送的TCP四次握手

   - 某个应用进程首先调用close主动关闭连接，这时TCP发送一个FIN M；

   - 另一端接收到FIN M之后，执行被动关闭，对这个FIN进行确认。它的接收也作为文件结束符传递给应用进程，因为FIN的接收意味着应用进程在相应的连接上再也接收不到额外数据；

   - 一段时间之后，接收到文件结束符的应用进程调用close关闭它的socket。这导致它的TCP也发送一个FIN N；

   - 接收到这个FIN的源发送端TCP对它进行确认。

     这样每个方向上都有一个FIN和ACK。

   ![img](https://raw.githubusercontent.com/c-sin7/picgoIMG/main/20190718155008892.png)



小明住在上海市长江路幸福小区5#666，现在小明在京东上面买了一部小米10Pro。京东在接到小米的订单后，工作人员从仓库中找到一部小米10Pro（应用层）。工作人员将手机打包好， 交给了京东物流（传输层）。接下来手机就到了转运中心（路由器），转运中心根据时间，成本等一系列因素决定下一步该发往哪一个转运中心(网络层)。决定好接下来发往哪一个转运中心后就开始用货车运输了，那么运输的过程就是数据链路层了，链路层负责将数据从一个端点送到另一个端点。那么货车行驶的道路就是物理层。几经周转，手机安全地送到了小明手上。

我们将一个小区比作一台计算机，一台计算机里面跑了很多程序，怎么区分程序呢，用的是端口，就好像小区用门牌号区分每一户人家一样。手机送到小明家了，怎么进去呢？从大门进啊，怎么找到大门呢？门牌号呀。不就相当于从互联网来的数据找到接收端计算机后再根据端口判断应该给哪一个程序一样吗。小明家的入口就可以用小区地址+门牌号进行唯一表示，那么同样的道理，程序也可以用IP+端口号进行唯一标识。那么这个程序的入口就被称作Socket。

