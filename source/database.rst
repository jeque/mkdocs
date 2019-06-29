数据库技能
======================
mysql数据库
---------------------

1.mysql数据库的安装
~~~~~~~~~~~~~~~~~~~~~~

mysql自定义路径二进制安装
###########################

安装路径：/Ultrapower/mysql-5.7.18

- 前期准备

检查环境::

 rpm -qa|grep libaio
 
如果没有，需要安装libaio::

 yum install -y libaio

创建mysql账户::

 useradd -s /bin/false -M mysql
 
下载mysql二进制包并解压::

 tar -zxf mysql-5.7.18-linux-glibc2.5-x86_64.tar.gz -C /Ultrapower/
 
切换到/Ultrapower目录，将mysql文件夹名改短,给mysql目录做一个软链接::

 cd /Ultrapower/
 
 mv mysql-5.7.18-linux-glibc2.5-x86_64/ mysql-5.7.18
 
 ln -s mysql-5.7.18/ mysql

在mysql目录下创建mysql-files，该文件夹权限为750，递归设置mysql目录的所属组和所属用户::
 
 mkdir mysql/mysql-files
 
 chmod 750 mysql/mysql-files
 
 chown -R mysql:mysql mysql-5.7.18/

- mysql目录内操作

初始化数据库,会在mysql目录内生成一个data目录，存放数据库的目录::

 cd mysql
 bin/mysqld --initialize --user=mysql --basedir=/Ultrapower/mysql --datadir=/Ultrapower/mysql/data
 
返回结果最后一行的末尾有随机密码，需要记下来。

`2017-04-28T02:49:00.853710Z 1 [Note] A temporary password is generated for root@localhost: wa0I:1w?V--a`

想设置默认密码为空则将--initialize选项替换为--initialize-insecure选项::
 
 bin/mysqld --initialize-insecure --user=mysql --basedir=/Ultrapower/mysql --datadir=/Ultrapower/mysql/data
 
安装ssl::

 bin/mysql_ssl_rsa_setup --datadir /Ultrapower/mysql/data/
 
指定data目录的路径,更改所属用户和组::

 chown -R root .
 
 chown -R mysql data mysql-files
 
除了mysql目录下的data目录和mysql-files目录所属用户不变，其他所有文件的所属用户改为root。

- 修改配置文件

执行命令::

 vi /etc/my.cnf

写入的内容为::

 [mysqld]
 
 datadir=/Ultrapower/mysql/data
 
 socket=/tmp/mysql.sock
 
 # Disabling symbolic-links is recommended to prevent assorted security risks
 
 symbolic-links=0
 
 # Settings user and group are ignored when systemd is used.
 
 # If you need to run mysqld under a different user or group,
 
 # customize your systemd unit file for mariadb according to the
 
 # instructions in https://fedoraproject.org/wiki/Systemd
 
 [mysqld_safe]
 
 log-error=/Ultrapower/mysql/data/err.log
 
 pid-file=/Ultrapower/mysql/data/mysql.pid
 
 # include all files from the config directory
 
拷贝启动程序::

 cp support-files/mysql.server /etc/init.d/mysql
 
将mysql的启动程序拷贝到/etc/init.d/目录下，以便启动程序,编辑启动文件，配置启动目录::

 sed -i 's#/usr/local/mysql#/Ultrapower/mysql#g' /etc/init.d/mysql
 
到这里mysql安装完成可以正常启动,启动命令为::

 service mysql start
 
- 后期结尾

命令创建软链接::

 ln -s /Ultrapower/mysql/bin/* /usr/local/sbin
 
登录mysql::

 mysql -u root -p
 Enter password: #输入之前保存的随机密码drRR0
 ...
 
修改密码sql语句::
 
 mysql> alter user 'root'@'localhost' identified by 'ultranms';
 mysql> quit

---------------------------------------------------------------------------------------------------------------------------------------------------------------

CentOS 7 下使用yum安装MySQL5.7.25
###################################

CentOS7默认数据库是mariadb, 但是 好多用的都是mysql ，但是CentOS7的yum源中默认好像是没有mysql的。安装前需要先准备mysql的yum源

- 下载mysql的repo源 这个安装的mysql5.7.25  /** 纠正一下，这源下载的是最新的版本 **/

运行如下命令::

 [root@localhost ~]# cd /usr/local/src/
 [root@localhost src]# wget http://repo.mysql.com/mysql57-community-release-el7-8.noarch.rpm

 [root@localhost src]# rpm -ivh mysql57-community-release-el7-8.noarch.rpm

 [root@localhost src]#  yum -y install mysql-server

 也可以指定安装目录     yum --installroot=/usr/local/mysql --releasever=/ -y install mysql-server）我没试， 这样装环境变量配置都不用你管， 装上直接启动就行。 安装路径是默认的。

安装完成后，需要配置文件路径。

默认配置文件路径::

 配置文件：/etc/my.cnf
 日志文件：/var/log/var/log/mysqld.log
 服务启动脚本：/usr/lib/systemd/system/mysqld.service
 socket文件：/var/run/mysqld/mysqld.pid 

- 配置my.cnf文件

执行命令::
        
 vim /etc/my.cnf
 
写入内容为::

     [mysqld]
    #
    # Remove leading # and set to the amount of RAM for the most important data
    # cache in MySQL. Start at 70% of total RAM for dedicated server, else 10%.
    # innodb_buffer_pool_size = 128M
    #
    # Remove leading # to turn on a very important data integrity option: logging
    # changes to the binary log between backups.
    # log_bin
    #
    # Remove leading # to set options mainly useful for reporting servers.
    # The server defaults are faster for transactions and fast SELECTs.
    # Adjust sizes as needed, experiment to find the optimal values.
    # join_buffer_size = 128M
    # sort_buffer_size = 2M
    # read_rnd_buffer_size = 2M
    datadir=/var/lib/mysql
    socket=/var/lib/mysql/mysql.sock
    server_id = 1
    expire_logs_days = 3

    # Disabling symbolic-links is recommended to prevent assorted security risks
    symbolic-links=0

    log-error=/var/log/mysqld.log
    pid-file=/var/run/mysqld/mysqld.pid
	
不过安装完成后，密码为随机密码，需要重置密码。

- 启动mysql服务,重置密码

执行命令::

 [root@localhost ~]# grep "password" /var/log/mysqld.log 
 
输入::

 mysql -u root -p   
 
输入密码-进入-第一次登陆 ，需要重置密码 要不什么也不能操作。

执行命令::

 alter user 'root'@'localhost' identified by 'Root!!2018'; 
 
 flush privileges;
 
授权::

 GRANT ALL PRIVILEGES ON *.* TO 'zabbix'@'%' IDENTIFIED BY 'Zabbix!123' WITH GRANT OPTION;
 
至此，mysql数据库就安装好了。

------------------------------------------------------------------------------------------------------------------------------------------

------------------------------------------------------------------------------------------------------------------------------------------

2.mysql端口号查看和修改
~~~~~~~~~~~~~~~~~~~~~~~~~

- Linux系统中限制用户su-权限的方法汇总
- glibc文件网站


------------------------------------------------------------------------------------------------------------------------------------------

3.mysql数据库备份-xtrabackup
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~



------------------------------------------------------------------------------------------------------------------------------------------

4.mysql数据库不能使用group by
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- linux系统下增加swap空间
- suse系统账号解锁
- awk 指定分隔符，读取csv格式的某些列


------------------------------------------------------------------------------------------------------------------------------------------

------------------------------------------------------------------------------------------------------------------------------------------

oracle数据库
---------------------

1.oracle数据库的优化
~~~~~~~~~~~~~~~~~~~~~~

2.查找数据库字符集和exp字符集
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

3.oracle11g plsql调试存储过程卡死的处理技巧
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

4.imp和exp数据导入导出
~~~~~~~~~~~~~~~~~~~~~~~~

5.扩展表空间及临时表空间
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

6.扩展表空间及临时表空间
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Redis数据库
---------------------

MongoDB数据库
---------------------

时序分析数据库Graphite
-------------------------

