---
layout: post
category: "python"
title: "利用virtualenv安装不同版本的Python"
tags: "Python"
---

声明：以下内容根据《Python开发实战》进行整理。

###1、virtualenv

安装virtualenv

    $ pip install virtualenv

安装完成后，使用帮助命令查看一下。

    $ virtualenv --help 

使用virtualenv建立虚拟运行环境

    $ export VIRTUALENV_USE_DISTRIBUTE=TRUE
    $ mkdir ~/work
    $ cd ~/work
    $ virtualenv env

上述命令执行后，会在work目录下建立一个新的env目录，这就是虚拟环境目录。  
VIRTUALENV_USE_DISTRIBUTE是向Distribute明示Python运行信息的环境变量。如果在开发过程中，希望所开发的Python应用程序有“不兼容旧版本的Python”或者“兼容最新版本Python”的要求，最好对该环境变量进行设定。为了不在每次登录都输入这样的命令，我们可以在登录的shell配置中加入下面这条语句。

    $ export VIRTUALENV_USE_DISTRIBUTE=TRUE

Distribute会根据这个环境变量是否存在，判断虚拟运行环境的配置有效或无效。因此在不使用Distribute的时候，建议用unset命令取消该环境变量。  
接下来，激活虚拟运行环境。

    $ source env/bin/activate

当使用了source命令后，虚拟运行环境信息开始生效。我们可以通过查看命令行终端开头是否出现了（env）这样的标志，来判断虚拟运行环境是否彻底被激活。如：

    (env)ubuntu:~/work$ 

检查安装好的包版本信息

    (env) $ pip freeze
    distribute==0.6.24
    wsgiref==0.1.2

可见，我们已经建立了一个安装最少数量包的Python虚拟运行环境。在这样的环境下，我们再一次使用pip install命令安装开发应用程序需要的包或者模块。如此以来，我们就可以很容易地把我在开发Python应用程序是需要安装的包和模块，从而尽可能减少其它不相干包或者模块给应用程序开发带来的位置影响。  
如果需要推出当前的虚拟运行环境，可以使用下面的命令。

    (env) $ deactivate

当不需要该虚拟环境时（这里就是指名为env的虚拟环境），可以直接使用rm等命令将对应的目录删除。

###2、virtualenvwrapper

接着我们介绍一种比virtualenv更容易使用的工具——virtualenvwrapper。virtualenv需要每次使用source命令导入虚拟运行环境信息，这一点非常麻烦，另外开发者还有可能忘记虚拟环境目录的建立位置。virtualenvwrapper这一命令行工具就是通过对virtualenv进行二次封装，解决了上述种种问题。  
####安装virtualenvwrapper

    $ pip install virtualenvwrapper

安装完成后，会在下面的位置生成virtualenvwrapper的shell脚本。  
/usr/local/bin/virtualenvwrapper.sh  
在使用virtualenvwrapper时，需要配置登录的shell初始化脚本，将virtualenvwrapper.sh的信息读入当前的shell环境。这里一bash为例，通过对用户目录下的.bashrc配置文件进行如下修改即可。

    if [ -f /usr/local/bin/virtualenvwrapper.sh ]; then
        export WORKON_HOME=$HOME/.virtualenvs
        source /usr/local/bin/virtualenvwrapper.sh
    fi

准备工作到此结束。由于.bashrc是在登录时执行的，因此如果登出了虚拟机上客户端操作系统，再一次登录之后，运行下面的命令同样可以使用virtualenvwrapper命令。  
再次读入.bashrc  

    source ~/.bashrc

我们可以输入命令mkvirtualenv，看一下起是否可用。

    $ mkvirtualenv --help

####使用

下面让我们一起看一下该工具的使用。和virtualenv一样，首先需要创建一个虚拟的运行环境。

    $ mkvirtualenv newenv

当输入上面命令后，也就和virtualenv一样，建立了一个虚拟的运行环境，而且一开始就处于激活的状态，但我们没有见到newenv目录。  
其实virtualenvwrapper对虚拟运行环境做了统一管理，根据上面配置的环境变量WORKON_HOME的路径信息，在其中建立了虚拟运行环境目录。在前面我们将WORKON_HOME设定为$HOME/.virtualenvs，让我们用下面的命令对这一目录进行确认，看一下是否有newenv目录生成。

    $ ls -la $HOME/.virtualenvs

退出虚拟运行环境对命令同样是deactivate，进入虚拟运行环境对命令变为workon。  
进入虚拟运行环境：

    $ workon newenv

当我们想浏览所有既存对虚拟运行环境却忘记了他们的名称时，可以不加任何选项，蛋蛋输入workon命令即可。虽然该工具包提供了lsvirtualenv这一专门浏览既存虚拟运行环境的命令，但如果仅仅是浏览环境，不如直接使用workon来的方便。  
通过mkvirtualenv建立的虚拟运行环境可用下面的命令删除。

    $ rmvirtualenv newenv

