---
author: Albert
date: 2015-07-06 23:00:00
layout: post
title: Cassandra(四):案例分享
categories: tech
---

>  没有最好,只有最适合. 

* 按报文大小排序->用户何时(When)在哪台(Where)机器接入哪个业务(What)?

<pre>
cqlsh:statistic> select 
             ... bytes,uid,occured_at,ip_address,sid,channel,tag,type  
             ... from 
             ... protocols_order_by_bytes 
             ... where 
             ... occured_on='2015-07-06' and bytes > 10000 
             ... limit 30;
</pre>

![query_case_01](http://atschx.b0.upaiyun.com/cassandra/cassandra_case_query_01.png)


