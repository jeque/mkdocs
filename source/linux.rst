Linux系统相关知识
======================

1.yum源配置方法
---------------------

**情景一、rhel6配置http yum源:**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
yum 是 yellowdog updater modified 简称,说白了就是升级版的rpm, yum的出现主要是由于rpm的那烦人的依赖关系所致,yum能够自动解决软件包之间的各种依赖关系。

yum大致的原理:
*当用户使用yum对软件包进行管理时,yum会依据它的配置文件到指定的yum源去下载所有在yum源中与软件包相关的元数据信息并将这些信息缓存到本地,然后依据这些信息对软件包的依赖性进行分析并尝试将其解决, 接着就是到yum源中下载相关的软件包到本地并开始安装*

注:

- yum的配置文件/etc/yum.conf和/etc/yum.repos.d/*.repo
- yum的本地缓存位置是在/etc/yum.conf当中定义的,默认位置为/var/cache/yum目录
- 元数据信息的存储位置是在yum源中的repodata目录当中
- 存储yum源位置一般是文件共享服务器(nfs, ftp, http),当然你的安装光盘镜像也能作为yum源

由于这里使用的是rhel 6.5 (Redhat Enterprise Linux 6.5),而红帽认为yum源是收费性的服务,所以我们必须删除原来安装系统时一并安装的yum才行,否则将出现如下信息

.. image:: https://raw.githubusercontent.com/jeque/mkdocs/master/images/image1.png

解决的方法就是把subscription-manager删除即可::
 
 # rpm -e subscription-manager

**配置网络http的yum源**

配置网络http的yum源比较简单,这里我们选择中国科技大学的yum源镜像站点,需要做的事情就是使用wget下载下面这个文件::

 # cd /etc/yum.repos.d/
 # wget -O CentOS-Base.repo https://lug.ustc.edu.cn/wiki/_export/code/mirrors/help/centos?codeblock=2
 
如果下载失败，可以将下面我准备好的`CentOS-Base.repo`文件放到`/etc/yum.repos.d/`中::

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
 name=CentOS-6 - Base - mirrors.ustc.edu.cn
 baseurl=http://mirrors.ustc.edu.cn/centos/6/os/$basearch/
 #mirrorlist=http://mirrorlist.centos.org/?release=6&arch=$basearch&repo=os
 gpgcheck=1
 gpgkey=http://mirrors.ustc.edu.cn/centos/RPM-GPG-KEY-CentOS-6
 #released updates
 [updates]
 name=CentOS-6 - Updates - mirrors.ustc.edu.cn
 baseurl=http://mirrors.ustc.edu.cn/centos/6/updates/$basearch/
 #mirrorlist=http://mirrorlist.centos.org/?release=6&arch=$basearch&repo=updates
 gpgcheck=1
 gpgkey=http://mirrors.ustc.edu.cn/centos/RPM-GPG-KEY-CentOS-6
 #additional packages that may be useful
 [extras]
 name=CentOS-6 - Extras - mirrors.ustc.edu.cn
 baseurl=http://mirrors.ustc.edu.cn/centos/6/extras/$basearch/
 #mirrorlist=http://mirrorlist.centos.org/?release=6&arch=$basearch&repo=extras
 gpgcheck=1
 gpgkey=http://mirrors.ustc.edu.cn/centos/RPM-GPG-KEY-CentOS-6
 #additional packages that extend functionality of existing packages
 [centosplus]
 name=CentOS-6 - Plus - mirrors.ustc.edu.cn
 baseurl=http://mirrors.ustc.edu.cn/centos/6/centosplus/$basearch/
 #mirrorlist=http://mirrorlist.centos.org/?release=6&arch=$basearch&repo=centosplus
 gpgcheck=1
 enabled=0
 gpgkey=http://mirrors.ustc.edu.cn/centos/RPM-GPG-KEY-CentOS-6
 #contrib - packages by Centos Users
 [contrib]
 name=CentOS-6 - Contrib - mirrors.ustc.edu.cn
 baseurl=http://mirrors.ustc.edu.cn/centos/6/contrib/$basearch/
 #mirrorlist=http://mirrorlist.centos.org/?release=6&arch=$basearch&repo=contrib
 gpgcheck=1
 enabled=0
 gpgkey=http://mirrors.ustc.edu.cn/centos/RPM-GPG-KEY-CentOS-6

保存并退出后,测试一下这个yum源是否能用, 先清空yum的缓存::

 # yum clean all
 # yum makecache
 
然后测试yum::

 # yum -y install vim
 
到此为此,我们的http网络yum源已经配置完成。

**情景二、rehl6.4 安装本地yum源:**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. role:: red

由于我们是在虚拟机中作测试,所以得用虚拟机模拟将光盘插入虚拟机的光驱中虚拟机(virtual machine) --> 设置(settings) --> CD/DVD(IDE),里指定操作系统的ISO镜像文件。
如果是物理机，则需要进入机房找到服务器，在光驱里面放入安装光盘。这个相对而言比较麻烦，所以一般最好复制光盘文件到本地硬盘。

.. image:: https://raw.githubusercontent.com/jeque/mkdocs/master/images/image2.png

然后再把光盘挂载到/media目录当中::

 # mount -r /dev/sr0 /media
 
接着就是要编辑yum的配置文件::

 # cd /etc/yum.repos.d/
 # vi rhel-media.repo
 
写入如下内容::

 [media]
  
 name=Red Hat Enterprise Linux 6.6                               
  
 baseurl=file:///mnt/cdrom                                        
  
 enabled=1                                                         
 
 gpgcheck=1                                                       
  
 gpgkey=file:///mnt/cdrom/RPM-GPG-KEY-redhat-release 

清除原有缓存::

 # yum clean all
 # yum makecache

这样我们本地光盘yum源就配置完成了。

**情景三、保留yum安装后的rpm包:**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
在linux上，使用yum安装，默认安装完成之后会删除下载的rpm包；想要yum安装软件后，还保留安装包，那么需要修改/etc/yum.conf配置文件中的keepcache参数::

 [root@bogon ~]# cat /etc/yum.conf 
 [main]
 cachedir=/var/cache/yum/$basearch/$releasever 【安装包保存位置】
 keepcache=0 【默认0是不保存安装包，改为1即可】
 debuglevel=2
 logfile=/var/log/yum.log
 exactarch=1
 obsoletes=1
 gpgcheck=1
 plugins=1
 installonly_limit=5
 bugtracker_url=http://bugs.centos.org/set_project.php?project_id=16&ref=http://bugs.centos.org/bug_report_page.php?category=yum
 distroverpkg=centos-release

使用vim或者sed修改::

 [root@bogon ~]# sed -n 's#keepcache=0#keepcache=1#gp' /etc/yum.conf 
 keepcache=1 【最好先不要用-i参数直接修改源文件，先输出看修改是否正确，或者先备份yum.conf配置文件】
 [root@bogon ~]# sed -i 's#keepcache=0#keepcache=1#g' /etc/yum.conf  【-i修改源文件配置】
 [root@bogon ~]# grep "keepcache" /etc/yum.conf【检查是否已修改】
 keepcache=1
 
把文件夹下的所有rpm包复制到指定文件夹::

 # cp $(find /var/cache/yum/ -name "*.rpm") /root/packages/ # 把下载的rpm包拷贝到你建的文件夹

2.文本编辑命令详解
---------------------

sed命令：sed是一种流编辑器，它是文本处理中非常中的工具，能够完美的配合正则表达式使用，功能不同凡响。处理时，把当前处理的行存储在临时缓冲区中，称为“模式空间”（pattern space），接着用sed命令处理缓冲区中的内容，处理完成后，把缓冲区的内容送往屏幕。接着处理下一行，这样不断重复，直到文件末尾。文件内容并没有 改变，除非你使用重定向存储输出。Sed主要用来自动编辑一个或多个文件；简化对文件的反复操作；编写转换程序等。

vi命令详解：vi命令是UNIX操作系统和类UNIX操作系统中最通用的全屏幕纯文本编辑器。Linux中的vi编辑器叫vim，它是vi的增强版（vi Improved），与vi编辑器完全兼容，而且实现了很多增强功能。

awk命令：awk是一种编程语言，用于在linux/unix下对文本和数据进行处理。数据可以来自标准输入(stdin)、一个或多个文件，或其它命令的输出。它支持用户自定义函数和动态正则表达式等先进功能，是linux/unix下的一个强大编程工具。它在命令行中使用，但更多是作为脚本来使用。awk有很多内建的功能，比如数组、函数等，这是它和C语言的相同之处，灵活性是awk最大的优势。

grep命令：grep（global search regular expression(RE) and print out the line，全面搜索正则表达式并把行打印出来）是一种强大的文本搜索工具，它能使用正则表达式搜索文本，并把匹配的行打印出来。

3.git仓库的安装与使用方法
---------------------
编译安装git 1.8：

4.制作qcow2镜像
---------------------

5.查看linux系统版本
----------------------

6.linux查看硬件信息命令和教程详解
----------------------------------

7.tar文件压缩解压方法
-----------------------

8.linux之间从本地复制文件到远程
---------------------------------

9.snmp安装方法
------------------

10.Linux系统下查看USB设备名及使用USB设备
----------------------------------------

11.AIX系统查CPU、内存
-------------------------

12.solaris下面查看route信息
-----------------------------

13.查看solaris防火墙
----------------------

14.Linux系统中限制用户su-权限的方法
------------------------------------

15.linux 2T以上磁盘分区创建与挂载
----------------------------------


