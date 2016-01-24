---
layout: post
category: "gae,tomcat,eclipse"
title:  "用eclipse本地部署GAE的demo时遇到的问题"
tags: [GAE,Tomcat,Eclipse]
---

这两天在尝试使用Google的GAE，参照Google提供的[App Engine Docs](https://cloud.google.com/appengine/docs)搭建本地的开发环境。  
学到了一些知识，也遇到了一些问题，这里就做一个简单的总结：  

###1、maven
首先，[maven](http://maven.apache.org)之前也有接触过，为了方便此项目的使用，这里就记录一些命令吧。  

    $ mvn -v --查看当前mvn的版本
    $ mvn appengine:devserver --编译并启动服务
    $ mvn appengine:devserver_start --启服务
    $ mvn appengine:devserver_stop --停服务
    $ mvn appengine:update --将项目上传到Google App Engine

这里需要说明的是，上传项目前，需要修改/src/main/webapp/WEB-INF/appengine-web.xml文件的application（project名）和version（版本）：

    <?xml version="1.0" encoding="utf-8"?>
    <appengine-web-app xmlns="http://appengine.google.com/ns/1.0">
      <application>YOUR-PROJECT-ID</application>
      <version>YOUR-VERSION-ID</version>
      <threadsafe>true</threadsafe>
    </appengine-web-app>

注：version需要符合一定的格式，对应的正则表达式：'^(?:^(?!-)[a-z\d\-]{0,62}[a-z\d]$)$'。  

###2、Eclipse部署Tomcat问题

####1) 启服务报java.io.FileNotFoundException:

    Could not resolve XML resource [null] with public ID [-//Oracle Corporation//DTD Web Application 2.3//EN], system ID [http://java.sun.com/dtd/web-app_2_3.dtd] and base URI [file:/D:/Program/apache-tomcat-8.0.26/webapps_prpall/appengine-try-java-master/WEB-INF/web.xml] to a known, local entity.

解决办法：修改conf/context.xml  

    <Context  xmlBlockExternal="false">

####2) 无法进入调试，并警告:  

    [SetPropertiesRule]{Server/Service/Engine/Host/Context} Setting property 'source' to 'org.eclipse.jst.jee.server:appengine-try-java-master' did not find a matching property.

解决办法：在Servers窗口中双击Tomcat，打开的窗口中找到并点击Open launch configuration，在Source中添加该project。  
