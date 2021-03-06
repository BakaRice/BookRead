## 第1章 初识Linux Shell

### 1.1 什么是Linux
linux 可以被划分成四个部分（Linux内核、GNU工具、图形化桌面环境、应用软件）

#### 1.1.1 深入探究Linux内核
内核主要负责以下四种功能：(系统内存管理、软件程序管理、硬件设备管理、文件系统管理)

1. 系统内存管理  
 内核不仅可管理可用的物理内存，还可以创建和管理虚拟内存（即不存在的内存）。  
 内核通过硬盘上的存储空间来实现虚拟内存，这块区域成为**交换空间(swap space)**
 内核会维护一个内存页面表，指名哪些页面位于物理内存中，哪些页面被交换到了磁盘上

2. 软件程序管理  
   Linux操作系统将运行中的程序成为*进程*，进程可以在前台运行，也可以在后台运行。   
   内核控制着Linux系统如何管理运行在系统上的所有进程。  
   内核创建了*第一个进程(init进程)*来启动系统章的所有其他进程

   Linux操作系统有五个启动运行级。
   运行级别为1是，只启动基本的系统进程以及一个控制台终端进程，我们称之为单用户模式。单用户模式通常用来在系统有问题时进行紧急的文件系统维护。
   标准的启动运行级别为3，在这个运行级上，大多数应用软件，比如网络支持程序，都会启动。另一个Linux场景的运行级是5，在这个运行级上系统会启动图形化的X Window系统，允许用户通过图形化桌面登录系统。

3. 硬件设备管理  
    任何Linux系统需要与之通信的设备，都需要在内核代码中加入其驱动程序代码。驱动程序代码相当于应用程序和硬件设备的中间人，允许内核与设备之间交换数据。
    在Linux内核中有两种方法用于插入设备驱动代码：
    - 编译进内核的设备驱动代码
    - 可插入内核的设备驱动模块
    
    Linux系统将硬件设备当成特殊的文件，成为**设备文件**,设备文件有3种分类：
    - 字符型设备文件
    - 块设备文件
    - 网络设备文件  

   字符型设备文件是指处理数据时每次只能处理一个字符的设备。大多数类型的调制解调器和终端都是作为字符型设备文件创建的。块设备文件是指处理数据时每次能处理大块数据的设备，比如硬盘。 
   网络设备是指采用数据包发送给和接收数据的设备，包括各种网卡和一个特殊的回环设备。这个回环设备允许Linux系统使用常见的网络编程协议同自身通信。
4. 文件系统管理  
   Linux内核支持通过不同类型的文件系统从硬盘种读写数据。除了自有的诸多文件系统外，Linux还支持从其他操作系统采用的文件系统中读写数据。内核必须在编译时就加入对所有可能用到的文件系统的支持，
  <table><thead><tr><th style="text-align:left;"><span>文件系统</span></th><th style="text-align:left;"><span>描述</span></th></tr></thead><tbody><tr><td style="text-align:left;"><span>ext</span></td><td style="text-align:left;"><span>Linux扩展文件系统，最早的Linux文件系统</span></td></tr><tr><td style="text-align:left;"><span>ext2</span></td><td style="text-align:left;"><span>第二扩展文件系统，在ext的基础上提供更多的功能</span></td></tr><tr><td style="text-align:left;"><span>ext3</span></td><td style="text-align:left;"><span>第三扩展文件系统，支持日志功能</span></td></tr><tr><td style="text-align:left;"><span>ext4</span></td><td style="text-align:left;"><span>第四扩展文件系统，支持高级日志功能</span></td></tr><tr><td style="text-align:left;"><span>hpfs</span></td><td style="text-align:left;"><span>OS/2高性能文件系统</span></td></tr><tr><td style="text-align:left;"><span>jfs</span></td><td style="text-align:left;"><span>IBM日志文件系统</span></td></tr><tr><td style="text-align:left;"><span>iso9660</span></td><td style="text-align:left;"><span>ISO 9660 文件系统(CD-ROM)</span></td></tr><tr><td style="text-align:left;"><span>minix</span></td><td style="text-align:left;"><span>MINIX文件系统</span></td></tr><tr><td style="text-align:left;"><span>msdoc</span></td><td style="text-align:left;"><span>微软的FAT16</span></td></tr><tr><td style="text-align:left;"><span>ncp</span></td><td style="text-align:left;"><span>Netware文件系统</span></td></tr><tr><td style="text-align:left;"><span>nfs</span></td><td style="text-align:left;"><span>网络文件系统</span></td></tr><tr><td style="text-align:left;"><span>ntfs</span></td><td style="text-align:left;"><span>支持micrsoft NT文件系统</span></td></tr><tr><td style="text-align:left;"><span>proc</span></td><td style="text-align:left;"><span>访问系统信息</span></td></tr><tr><td style="text-align:left;"><span>ReiserFS</span></td><td style="text-align:left;"><span>高级Linux文件系统，能提供更好的性能和硬盘恢复功能</span></td></tr><tr><td style="text-align:left;"><span>smb</span></td><td style="text-align:left;"><span>支持网络访问的Samba SMB文件系统</span></td></tr><tr><td style="text-align:left;"><span>sysv</span></td><td style="text-align:left;"><span>较早期的Unix文件系统</span></td></tr><tr><td style="text-align:left;"><span>ufs</span></td><td style="text-align:left;"><span>BSD文件系统</span></td></tr><tr><td style="text-align:left;"><span>umsdos</span></td><td style="text-align:left;"><span>建立在msdos上的类Unix文件系统</span></td></tr><tr><td style="text-align:left;"><span>vfat</span></td><td style="text-align:left;"><span>Windows 95文件系统（FAT32)</span></td></tr><tr><td style="text-align:left;"><span>XFS</span></td><td style="text-align:left;"><span>高性能64位日志文件系统</span></td></tr></tbody></table>

   Linux内核采用虚拟文件系统（Virtual File System，VFS)作为和每个文件系统交互的接口。这为Linux内核同任何类型文件系统通信提供了一个标准接口。当每个文件系统都被挂载和使用时。VFS将信息都缓存在内存中。


#### 1.1.2 GNU工具


+ 核心GNU工具
  GNU coreutils软件包由三部分构成：
  - 用以处理文件的工具
  - 用以操作文本的工具
  - 用以管理进程的工具
+ shell  
   GNU/Linux shell 是一种特殊的交互式工具，它为用户提供了启动程序、管理文件系统章的文件以及运行在Linux系统上的进程的途径。Shell的核心是命令行提示符。命令行提示符是shell负责交互的部分。它允许你输入文本命令，然后解释命令，并在内核种执行。


#### 1.1.3 Linux桌面环境

...

### 1.2 Linux发行版本

...

