---
layout: post
category: ["eclipse", "tomcat"]
title: "Maven项目在Eclipse中，Tomcat的Add And Remove找不到项目"
tags: ["Eclipse", "Tomcat"]
---

#### 1、右键项目 -> Properties -> Project Facets  

勾选Dynamic web module，如果无法点击确定，根据提示在勾选要求勾选的项（例如我的项目还要求勾选Java 1.6 or newer）即可。  

#### 2、右键项目 -> Properties -> Deployment Assembly  

修改如下图：  

![Deployment Assembly](/images/eclipse-tomcat-add-and-remove-001.jpg) 
