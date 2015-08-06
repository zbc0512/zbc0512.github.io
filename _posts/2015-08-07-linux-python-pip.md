---
layout: post
category: "Python"
title: "Linux中Python3.4.3下pip不好使"
tags: ["Linux", "Python"]
---

从 Python 3.4 开始就已经自带了 pip 和 easy_install（setuptools 包带的命令）包管理命令  
添加 python3.4 到环境变量，编辑 ~/.bash_profile，将：  

    PATH=$PATH:$HOME/bin  
    改为：  
    PATH=$PATH:$HOME/bin:/usr/local/python34/bin  

使 python3.4 环境变量生效：  

    # . ~/.bash_profile  
