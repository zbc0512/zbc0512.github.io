---
layout: post
category: ["eclipse", "tomcat"]
title: "在Eclipse中配置Tomcat8.5.x"
tags: ["Eclipse", "Tomcat"]
---

因为eclipse中配置tomcat的时候，eclipse会去获取tomcat的版本（[Tomcat 8.5.x 分支来自于Tomcat 9.0.0 M4](http://tomcat.apache.org/tomcat-8.5-doc/changelog.html)），所以我们只要做个伪装骗过eclipse即可。  

首先先进入到tomcat的lib目录。  

#### 方法一：

找到catalina.jar，打开catalina.jar/org/apache/catalina/util/ServerInfo.properties文件，修改server.info的参数：  

    server.info=Apache Tomcat/9.0.5

#### 方法二：

在lib目录下创建如下目录：  

    org/apache/catalina/util

将方法一中找到的ServerInfo.properties文件复制到此目录，修改server.info的参数：  

    server.info=Apache Tomcat/9.0.5

然后在eclipse中，按照9.0的tomcat去配置就行了。
