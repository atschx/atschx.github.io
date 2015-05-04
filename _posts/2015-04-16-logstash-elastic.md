---
author: Albert
date: 2015-04-16 17:45:43+00:00
layout: post
title:  日志·Log(Timestamp+Data)
categories: elk
---

> Log = Timestamp + Data.
<a href="http://logstash.net"><img alt="logstash" src="http://7xil0c.com1.z0.glb.clouddn.com/logstash.png" width="76" height="121" /></a>

解决生产环境中的问题：`分析下日志吧！` *满屏密密麻麻的字符串亮瞎眼....*

Intro ELK
---------

背景资料:**`Logstash`**出自世界著名的运维工程师乔丹西塞(JordanSissel)之手，诞生于2009 年 8 月 2 日。**`Elasticsearch`**近两年最受关注的大数据项目之一，开始于2010年。**`Kibana`**是一个使用Apache开源协议的Elasticsearch分析和搜索仪表板。2013 年，Logstash 被 Elasticsearch 公司收购，ELK stack 正式成为官方用语.

>  Using Elasticsearch as a backend datastore, and kibana as a frontend reporting tool, Logstash acts as the workhorse, creating a powerful pipeline for storing, querying and analyzing your logs. With an arsenal of built-in inputs, filters, codecs and outputs, you can harness some powerful functionality with a small amount of effort. 

Logstash
--------

<img alt="logstash" src="http://7xidkg.com1.z0.glb.clouddn.com/logstash-architecture.png" width="572" height="323" />

shipper等价于应用机器上的agent，通过监听`事件`统一规整到Broker(相当于一个buffer)，indexer是就是logstash的server部分。本身上来讲logstash不细分角色，其input-filter-output的机制，灵活度很高。对于Storage部分，Elasticsearch提供了全文索引，最后通过Kibana展现。

一个符合SLA协议的部署结构大致可以是这样的，官方参考。

<img alt="logstash" src="http://7xidkg.com1.z0.glb.clouddn.com/logstash-architecture-final.png" width="572" height="323" />

Elasticsearch
-------------

推荐几个插件:

* elastic-head
* bigdesk
* paramedic

Collectd
--------

> 5月1号，留意到colletd，精悍。使用`collectd`收集服务器的状态信息，get.

<img alt="collectd" src="{{ site.baseurl }}/assets/images/collectd_memory.png" />

Test
-----

> bin/logstash -e 'input { stdin { } } output { elasticsearch { host => localhost } }'

![snapshot](http://7xidkg.com1.z0.glb.clouddn.com/snapshot-logstash.png)

参考资料
--------

* [Elasticsearch:The Definitive Guide](http://www.elastic.co/guide/en/elasticsearch/guide/current/index.html)
* [The_LogStash_Book](http://www.logstashbook.com/code/index.html)
* [Kibana 中文指南](http://kibana.logstash.es/)
* [elasticsearch 权威指南](https://github.com/GavinFoo/elasticsearch-definitive-guide)
* [Logstash 最佳实践](https://github.com/chenryn/logstash-best-practice-cn)

github
-------

* [elasticsearch](https://github.com/elastic/elasticsearch)
* [logstash](https://github.com/elastic/logstash)
* [kibana](https://github.com/elastic/kibana)

> Remember: if a new user has a bad time, it's a bug in logstash.

1. http://www.cnblogs.com/vovlie/p/4227027.html
2. http://www.firefoxbug.com/index.php/category/logstash--e6-9c-8d-e5-8a-a1-e5-99-a8/
3. http://ju.outofmemory.cn/entry/113144

案例分享
-------

日志格式

	10.10.50.68 - - [17/Apr/2015:22:20:54 +0800] "POST /im-daos/dao/ims/chat HTTP/1.1" 200 16 2

grok(http://grokdebug.herokuapp.com/)表达式

	%{IPORHOST:clientip} %{USER:ident} %{USER:auth} \[%{HTTPDATE:timestamp}\] "(?:%{WORD:verb} %{NOTSPACE:request}(?: HTTP/%{NUMBER:httpversion})?|%{DATA:rawrequest})" %{NUMBER:response} (?:%{NUMBER:bytes}|-) (?:%{NUMBER:mills}|-)
