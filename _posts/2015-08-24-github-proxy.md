---
layout: post
category: "github"
title: "GitHub代理设置"
tags: "GitHub"
---

在Git Shell中输入如下命令：  

    cd ~

发现home路径是C:\Users\z，在C:\Users\z目录下找到文件.gitconfig，里面内容如下：  

    [user]
    name = zbc
    email = zbc0512@163.com
    [http]
    proxy = http://host:port
    [https]
    proxy = http://host:port

修改代理部分，重启GitHub客户端，发现代理已经可以使用，可以正常push代码了。  

<font color="#F00">注：此方法为GitHub代理设置的通用方法，与任何公司（例如PICC）内网无关，在此声明，敬请知晓！</font>  
