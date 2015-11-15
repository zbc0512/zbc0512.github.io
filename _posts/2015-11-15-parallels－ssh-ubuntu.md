---
layout: post
category: "linux"
title: "Parallels虚拟机下通过ssh访问Ubuntu"
tags: [Linux,Ubuntu]
---

Ubuntu中，利用如下命令查看一下Ubuntu的ip：  

    ifconfig

会显示两个网卡信息，eth0和lo。  
eth0对应的ip就是为Ubuntu所分配的一个临时ip地址。  
在本地电脑利用ssh远程客户端访问这个地址即可。  
