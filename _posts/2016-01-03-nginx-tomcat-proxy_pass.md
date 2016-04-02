---
layout: post
category: "nginx,tomcat"
title:  "Nginx反向代理Tomcat"
tags: [Nginx,Tomcat]
---

### 1、配置Tomcat
假设要通过Nginx来访问Tomgcat下的test项目，先把Tomcat配置成默认访问test，这样我们访问http://localhost:8080时，就可以直接访问test了  
参考：<http://zbc.io/tomcat/tomcat-path.html>  

### 2、配置Nginx
编辑nginx下的nginx.conf文件  
在http中配置upstream，用来配置要转发的URL  

        upstream tomcat{
                server 127.0.0.1:8080;
        }

在server中配置server_name和location  

        server_name localhost;
        location / {
                #指向配置的upstream
                proxy_pass http://tomcat;
        }

        location ~ \.(jsp|do)$ {
                #处理jsp文件和.do的请求
                proxy_pass http://tomcat;
        }

        location ~ \.(html|js|css|gif|jpg|jpeg|png|bmp|ico))$ {
                #处理静态文件
                root /srv/apache-tomcat-8.0.26/webapps/test/;
                #设置过期时间
                expires 12h;
        }

这时就可以用localhost来直接访问test了。
