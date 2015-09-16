---
layout: post
category: "tomcat"
title: "Tomcat项目路径配置"
tags: "Tomcat"
---

Tomcat对工程的部署一般是将工程的压缩文件放在tomcat安装目录的webapps下，访问时通过键入： 

    http://localhost:8080/xx(假定为本机访问，xx是部署时的应用工程的访问名字）。

而如果直接键入：http://localhost:8080出来的将是tomcat自带的欢迎页面，如何让键入http://localhost:8080出来的是自己的应用工程的页面呢？  
  
在Tomcat默认安装后，tomcat的主目录是webapps/root目录，所以如果想改变tomcat的主目录的话可以如下所做：  

####方法一：
（假设tomcat安装在C盘下，项目名为bidding）打开C:/Tomcat/conf/server.xml，在<host></host>之间加入代码：  

    <Context docBase="C:/Program Files/Apache Software Foundation/Tomcat 5.5/webapps/bidding" path="" debug="0"  reloadable="true"/>

这样重新启动tomcat，我们的主目录就被设置为bidding这个项目了。  

####方法二：
将tomcat安装目录下的ROOT下的所有文件全部删除，然后将工程的解压后的文件全部拷进去。  

####方法三：
Tomcat5.0以下版本在C:/Tomcat/conf/Catalina/localhost目录下会自动生成了一个ROOT.Xml，但是5.0以上版本不再生成此文件，所以可以新建个ROOT.xml,在里面加入如下代码：  

    <?Xml version='1.0' encoding='utf-8'?>
    <Context crossContext="true" docBase=""C:/Program Files/Apache Software Foundation/Tomcat 5.5/webapps/bidding"" path="" reloadable="true"></Context>

参考链接：<http://jingyan.baidu.com/article/3c343ff7099ee40d37796307.html>
