---
layout: post
category: "python"
title: "Linux中Python3.4.3下pip不好使"
tags: ["Linux", "Python"]
---

###方法一：
由于pip是针对python2使用的，因此在Python3里面需要使用pip3。  

###方法二：
也可以建立一个新的链接来指向pip3：  

    ln -s /usr/local/python-3.4.3/bin/pip3 /usr/bin/pip
