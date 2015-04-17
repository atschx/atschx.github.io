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

Setup
-----

1. Install Logstash
	* ruby1.8.7 
	* curl -O https://download.elasticsearch.org/logstash/logstash/logstash-1.4.2.tar.gz
	* tar zxvf logstash-1.4.2.tar.gz && cd logstash-1.4.2 
	* bin/logstash -e 'input { stdin { } } output { stdout {} }'
2. Install Elasticsearch 
	* ununtu下可以直接采用apt方式
	* 下载后手动start
3. Install Kibana (这个安装最简单,启动时要求已启动Elasticsearch

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

http://www.cnblogs.com/vovlie/p/4227027.html
http://www.firefoxbug.com/index.php/category/logstash--e6-9c-8d-e5-8a-a1-e5-99-a8/
http://ju.outofmemory.cn/entry/113144
