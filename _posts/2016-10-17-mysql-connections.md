---
layout: post
category: "mysql"
title: "MySQL连接数"
tags: "MySQL"
---

#### 1、设置最大连接数：  

##### 方法一、使用mysql命令：  

    查看最大连接数：
    show variables like 'max_connections';

    查看响应的最大连接数：
    show global status like 'Max_used_connections';

    设置最大连接数：
    set GLOBAL max_connections=连接数;

##### 方法二、修改/etc/my.cnf中的max_connections

#### 2、show status：  

    Threads_connected  当前的连接数
    Connections  试图连接到(不管是否成功)MySQL服务器的连接数。
    Max_used_connections  服务器启动后已经同时使用的连接的最大数量。

#### 3、显示当前mysql状态：  

    mysql> status                                                                                                                                                                               
    --------------                                                                                                                                                                              
    mysql  Ver 14.14 Distrib 5.6.33, for linux-glibc2.5 (x86_64) using  EditLine wrapper                                                                                                        

    Connection id:          1107720                                                                                                                                                             
    Current database:                                                                                                                                                                           
    Current user:           root@localhost                                                                                                                                                      
    SSL:                    Not in use                                                                                                                                                          
    Current pager:          stdout                                                                                                                                                              
    Using outfile:          ''                                                                                                                                                                  
    Using delimiter:        ;                                                                                                                                                                   
    Server version:         5.6.33 MySQL Community Server (GPL)                                                                                                                                 
    Protocol version:       10                                                                                                                                                                  
    Connection:             Localhost via UNIX socket                                                                                                                                           
    Server characterset:    latin1                                                                                                                                                              
    Db     characterset:    latin1                                                                                                                                                              
    Client characterset:    utf8                                                                                                                                                                
    Conn.  characterset:    utf8                                                                                                                                                                
    UNIX socket:            /tmp/mysql.sock                                                                                                                                                     
    Uptime:                 7 days 3 hours 58 min 4 sec                                                                                                                                         

    Threads: 28  Questions: 8621582  Slow queries: 0  Opens: 73  Flush tables: 1  Open tables: 66  Queries per second avg: 13.926                                                               
    --------------  
