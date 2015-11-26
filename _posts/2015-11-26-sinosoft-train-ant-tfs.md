---
layout: post
category: [ant,TFS]
title: "TFS下的打包发布"
tags: [Ant,TFS]
---

##一、Ant

###1、Ant的安装与配置

下载安装包并解压至某目录，例如：D:\apache-ant-1.9.5，然后配置环境变量：  

    ANT_HOME: D:\apache-ant-1.9.5
    Path: %ANT_HOME%\bin

###2、Hello World

Ant的构件文件是基于XML编写的，默认名称为build.xml，执行ant命令默认寻找build.xml；  
也可以自己指定这个文件,例如：  

    ant -f a.xml

举个栗子，在a.xml中添加如下代码：  

    <?xml version="1.0"?>
    <project name="helloWorld">
      <target name="hello">
        <echo message="Hello,百成"/>
      </target>
    </project>

然后执行如下命令：  

    ant -f a.xml hello

意思就是指定Ant的构建文件为a.xml，执行名称为hello这个target。  
也可以指定默认的target，只需做如下修改：  

    <?xml version="1.0"?>
    <project name="helloWorld" default="hello">
      <target name="hello">
        <echo message="Hello,百成"/>
      </target>
    </project>

这是只需执行如下命令：  

    ant -f a.xml

如果再把文件名改回build.xml，则只需执行ant即可。  































