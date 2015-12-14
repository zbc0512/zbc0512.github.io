---
layout: post
category: [python]
title: "批量将文件名中的大写字母替换为小写"
tags: [Python]
---

场景：  
个人文件夹里有一些文件的文件名全为大写的，十分不便于阅读，就想有什么办法能把他们全部变成小写的呢？  
刚好最近在学习Python，就用Python来完成这件事吧！  
代码如下：  

    #批量将文件名全部转换为小写，可修改path来自定义文件目录
    import os
    
    def rename_file():
        path = "D:/"
        file_list = os.listdir(path)
        for file_name in file_list:
            file_name_old = path + file_name
            file_name_new = path + file_name.lower()
            os.rename(file_name_old, file_name_new)

