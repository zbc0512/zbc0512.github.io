---
layout: post
category: "maven"
title: "开源中国 Maven 库使用帮助"
tags: "Maven"
---

[开源中国 Maven 库使用帮助](http://maven.oschina.net/help.html)

注：该帮助文档中有如下命令，来生成maven项目：

    mvn archetype:create -DgroupId=oschina -DartifactId=simple -DpackageName=net.oschina.simple  -DarchetypeArtifactId=maven-archetype-webapp -DinteractiveMode=false

但在我的电脑上使用上述命令生成maven项目时，报如下错误：

    [ERROR] Failed to execute goal org.apache.maven.plugins:maven-archetype-plugin:2
    .4:create (default-cli) on project standalone-pom: Unable to parse configuration
     of mojo org.apache.maven.plugins:maven-archetype-plugin:2.4:create for paramete
    r #: Cannot create instance of interface org.apache.maven.artifact.repository.Ar
    tifactRepository: org.apache.maven.artifact.repository.ArtifactRepository.<init>
    () -> [Help 1]
    [ERROR]
    [ERROR] To see the full stack trace of the errors, re-run Maven with the -e swit
    ch.
    [ERROR] Re-run Maven using the -X switch to enable full debug logging.
    [ERROR]
    [ERROR] For more information about the errors and possible solutions, please rea
    d the following articles:
    [ERROR] [Help 1] http://cwiki.apache.org/confluence/display/MAVEN/PluginConfigur
    ationException

原因是在maven3.0.5以上版本舍弃了create，使用generate生成项目  

参考：<http://bbs.csdn.net/topics/391016527>
