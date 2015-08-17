---
layout: post
category: "django"
title: "Linux上启动Django之后，外部无法访问"
tags: "Django"
---

####原因：  
默认情况只允许本机IP访问。  

####解决：  
运行如下命令来启动Django，即可接收所有IP访问：  

    python manage.py runserver 0.0.0.0:8000
