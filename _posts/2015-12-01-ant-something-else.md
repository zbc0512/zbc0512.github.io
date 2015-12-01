---
layout: post
category: [ant]
title: "Ant一些其他的"
tags: [Ant]
---

###Ant删除


    <delete includeemptydirs="true">
        <fileset dir="build" includes="**/*" excludes="webapp_jar_history/*,webapp*.jar,webapp*.txt"/>
    </delete>

includeemptydirs：是否包含空目录  
fileset：指定目录，dir指定delete在哪个目录下进行操作，其中includes和excludes可以选择包含和排除的目录  
注：其中的"\*"是通配符，"\**"表示匹配任何内容  
