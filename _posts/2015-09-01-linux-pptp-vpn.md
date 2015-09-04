---
layout: post
category: "linux"
title: "centos6.4安装搭建pptp vpn服务"
tags: "Linux"
---

在网上找了好多资料，写的都不尽相同，也不是很详尽，所以自己重新整理了一下。  
###一、环境
操作系统：CentOS 7.0 64位  
本地网卡：  

    # ifconfig
    eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
          inet 10.172.96.8  netmask 255.255.248.0  broadcast 10.172.103.255
    eth1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
          inet 47.88.1.245  netmask 255.255.252.0  broadcast 47.88.3.255

说明：本地网卡eth0负责连接vpn客户端，eth1负责与10.100.100.0网段服务器的连接。  
目的：  
1. vpn客户端能够成功的连接到vpn服务器上；  
2. vpn服务器可以转发来自vpn客户端对10.100.100.0网段的请求。  
检查是否支持：  

    # modprobe ppp-compress-18 && echo ok

执行上述命令后，显示“ok”。继续执行如下命令，并提示如下信息，则表明支持。  

    # cat /dev/net/tun
    cat: /dev/net/tun: File descriptor in bad state

上述两条均通过，才能安装pptp。否则就只能考虑openvpn。  
###二、安装
1. Cent OS 7.0 默认集成了MPPE和PPP，以及iptables，因此下面检查也可以忽略：  

    # rpm -q ppp // 查询当前系统的ppp是否默认集成了，以及ppp的版本

用以下命令检查PPP是否支持MPPE：

    # strings '/usr/sbin/pppd' |grep -i mppe | wc --lines

如果以上命令输出为“0”则表示不支持；输出为“30”或更大的数字就表示支持，MPPE（Microsoft Point to Point Encryption，微软点对点加密）。  
2. 安装pptpd

    # yum install pptpd

也可以自行下载进行安装：  

    # rpm -ivh pptpd-1.4.0-1.el6.x86_64.rpm

64位pptpd-1.4.0-1.el6.x86_64.rpm的下载地址：<http://www.pipipan.com/file/18457333>  
32位pptpd-1.4.0-1.el6.i686.rpm版本下载地址：<http://www.400gb.com/file/54124192>  

###三、配置
注：配置相应文件时建议先使用cp命令备份.bak文件。
####1. 配置/etc/ppp/options.pptpd
去掉两行ms-dns前面的#，并修改为google的dns  

    ms-dns 8.8.8.8
    ms-dns 8.8.4.4

####2. 配置/etc/ppp/chap-secrets
用户登录信息：  

    username    pptpd    password    *

####3. 配置/etc/pptpd.conf
去掉localip和remoteip两行的注释：  

    localip 192.168.0.1
    remoteip 192.168.0.234-238,192.168.0.245

####4. 配置/etc/sysctl.conf
在末尾添加下面的代码，使内核支持转发：  

    net.ipv4.ip_forward = 1

运行下面的命令使内核修改生效：  

    # sysctl -p

###四、转发
添加下面的iptables转发规则  

    iptables -t nat -A POSTROUTING -s 192.168.0.0/24 -o eth1 -j MASQUERADE

注意：由于阿里云是双网卡，内网eth0，外网eth1，所以这块特别容易误写为eth0，这也是为什么很多杂乱的教程无法配置成功的原因之一。  

添加转发规则后重启就会失效，CentOS 6系统可以使用service iptables save保存配置，但CentOS 7不支持，可能会报错：  

    -bash: /etc/init.d/iptables: No such file or directory

我们需要将配置写入rc.local文件中，开机自动设置，运行下面的命令赋予rc.loacl执行权限：  

    chmod +x /etc/rc.d/rc.local

然后编辑rc.local，并把上面的转发规则写到文件末尾。  

###五、启动
####1. 启动pptpd

    /etc/init.d/pptpd start

####2. 用下面的命令使pptpd开机自动启动

    chkconfig pptpd on

到此为止，vpn已搭建完成，可以连接并访问外网了。  

###参考：  
centos6.4安装搭建pptp vpn服务：<http://blog.csdn.net/musiccow/article/details/22655637>  
centos6.4安装配置vpn服务器步骤详解：<http://www.jb51.net/os/RedHat/128137.html>
阿里云服务器配置VPN详解，pptpd下载地址更新版：<http://bbs.aliyun.com/read/231812.html>  
Centos 7搭建VPN（PPTP）服务器方法：<http://www.wanghailin.cn/centos-7-vpn/>  