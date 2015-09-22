---
layout: post
category: "informix"
title: "Informix关联外键"
tags: "Informix"
---

今天工作中遇到的问题，把公司的数据库迁移到另一个服务器，执行关联外键的SQL时，报错：  

    525: Failure to satisfy referential constraint fk_msg_bra_t_c_veh.
      111: ISAM error:  no record found.

后来发现是因为一个表有数据，而另一个表没有数据，在没有数据的表中插入相应数据后，执行成功。

