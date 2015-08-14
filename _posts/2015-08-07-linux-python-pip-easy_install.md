---
layout: post
category: "python"
title: "Linux中Python3.4.3下pip和easy_install不好使"
tags: ["Linux", "Python"]
---

###pip
####方法一：
由于pip是针对python2使用的，因此在Python3里面需要使用pip3。  

####方法二：
也可以建立一个新的链接来指向pip3：  

    ln -s /usr/local/python-3.4.3/bin/pip3 /usr/bin/pip

###easy_install同理：
如果提示如下信息：  

    ln: creating symbolic link `/usr/bin/easy_install': File exists

只需将原来的easy_install命名为easy_install_old，然后再创建链接即可：  

    mv /usr/bin/easy_install /usr/bin/easy_install_old
    ln -s /usr/local/python-3.4.3/bin/easy_install-3.4 /usr/bin/easy_install
