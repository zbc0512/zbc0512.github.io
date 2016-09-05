---
layout: post
category: ["eclipse", "tomcat"]
title: "在Eclipse中配置Tomcat8.5.4"
tags: ["Eclipse", "Tomcat"]
---

首先先进入到tomcat的lib目录。  

###方法一：

找到catalina.jar，打开catalina.jar/org/apache/catalina/util/ServerInfo.properties文件，修改server.info的参数：  

    server.info=Apache Tomcat/8.0.54

###方法二：

在lib目录下创建如下目录：  

    org/apache/catalina/util

将方法一中找到的ServerInfo.properties文件复制到此目录，修改server.info的参数：  

    server.info=Apache Tomcat/8.0.54

然后在eclipse中，按照8.0的tomcat去配置就行了。
