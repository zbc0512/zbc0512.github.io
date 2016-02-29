---
layout: post
category: "linux"
title: "Linux下安装mysql"
tags: "Linux"
---

#### linux安装mysql服务分两种安装方法：
1. 源码安装，优点是安装包比较小，只有十多M，缺点是安装依赖的库多，安装编译时间长，安装步骤复杂容易出错；  
2. 使用官方编译好的二进制文件安装，优点是安装速度快，安装步骤简单，缺点是安装包很大，300M左右。以下介绍linux使用官方编译好的二进制包安装mysql。  

MySQL mirrors地址：<http://dev.mysql.com/downloads/mirrors.html>  

### 一、准备工作：
下载官方编译好的二进制包并解压：  

    wget ftp://ftp.jaist.ac.jp/pub/mysql/Downloads/MySQL-6.0/mysql-6.0.11-alpha-linux-x86_64-glibc23.tar.gz
    tar -xzvf mysql-6.0.11-alpha-linux-x86_64-glibc23.tar.gz

复制解压后的mysql目录到系统的本地软件目录：  

    cp mysql-6.0.11-alpha-linux-x86_64-glibc23 /usr/local/mysql -r

注意：此处建议用如下方法，使用软链过去，不要直接包文件复制，便于系统安装多个版本的mysql：  

    cp mysql-6.0.11-alpha-linux-x86_64-glibc23 /usr/local/
    ln -s mysql-6.0.11-alpha-linux-x86_64-glibc23 mysql

### 二、用户和组：
添加系统mysql组和mysql用户：  

    groupadd mysql
    useradd -r -g mysql mysql

进入安装mysql软件目录：  

    cd /usr/local/mysql

修改当前目录所属的组mysql和用户mysql：  

    chgrp -R mysql .
    chown -R mysql:mysql .

### 三、开始安装：
安装数据库：

    scripts/mysql_install_db --user=mysql

将mysql/目录下除了data/目录的所有文件，改回root用户所有，mysql用户只需作为mysql/data/目录下所有文件的所有者：

    chown -R root .
    chown -R mysql data

### 四、开机启动：
复制mysql配置文件：

    cp support-files/my-medium.cnf /etc/my.cnf

首先需要将scripts/mysql.server服务脚本复制到/etc/init.d/，并重命名为mysqld：  

    cp support-files/mysql.server /etc/init.d/mysqld

通过chkconfig命令将mysql服务加入到自启动服务项中，注意服务名称mysql就是我们将mysql.server复制到/etc/init.d/时重命名的名称：  

    chkconfig --add mysqld

查看是否添加成功：  

    chkconfig --list mysqld

重启系统，mysqld就会自动启动了。检查是否启动：  

    netstat -anp|grep mysqld

显示如下：  

    tcp        0      0 0.0.0.0:3306                0.0.0.0:*                   LISTEN      27628/mysqld
    unix  2      [ ACC ]     STREAM     LISTENING     204207 27628/mysqld        /tmp/mysql.sock

如果不想重新启动系统，那就手动启动MySQL服务：  

    service mysqld start

### 五、其他配置：
将/usr/local/mysql/bin/mysql加入环境变量中，在/etc/profile最后加入两行命令：

    MYSQL_HOME=/usr/local/mysql
    export PATH=$PATH:$MYSQL_HOME/bin

修改mysql的root用户密码，root初始密码为空的：

    /usr/local/mysql/bin/mysqladmin -u root password '密码'

### 六、参考链接：
<http://jingyan.baidu.com/article/a378c9609eb652b3282830fd.html>  
<http://blog.csdn.net/wendi_0506/article/details/39478369>  
<http://blog.csdn.net/superchanon/article/details/8546254>  
