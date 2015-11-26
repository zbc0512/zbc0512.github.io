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

###3、一些关键元素

####1.project元素
project元素是Ant构件文件的根元素，Ant构件文件至少应该包含一个project元素，否则会发生错误。  
在每个project元素下，可包含多个target元素。  
#####1) name属性：  
用于指定project元素的名称。  
#####2) default属性：  
用于指定project默认执行时所执行的target的名称。  
#####3) basedir属性：  
用于指定基路径的位置。该属性没有指定时，使用Ant的构件文件的附目录作为基准目录。  

####2.target元素
它为Ant的基本执行单元，它可以包含一个或多个具体的任务。多个target可以存在相互依赖关系。它有如下属性：  
#####1)name属性：  
指定target元素的名称，这个属性在一个project元素中是唯一的。我们可以通过指定target元素的名称来指定某个target。  
#####2)depends属性：  
用于描述target之间的依赖关系，若与多个target存在依赖关系时，需要以“,”间隔。Ant会依照depends属性中target出现的顺序依次执行每个target。被依赖的target会先执行。  
#####3)if属性：  
用于验证指定的属性是否存在，若不存在，所在target将不会被执行。  
#####4)unless属性：  
该属性的功能与if属性的功能正好相反，它也用于验证指定的属性是否存在，若不存在，所在target将会被执行。  
#####5)description属性：  
该属性是关于target功能的简短描述和说明。

####3.property元素
该元素可看作参量或者参数的定义，project的属性可以通过property元素来设定，也可在Ant之外设定。  
若要在外部引入某文件，例如build.properties文件，可以通过如下内容将其引入：  

    <property file=” build.properties”/>












