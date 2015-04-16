---
author: Albert
date: 2015-04-16 17:45:43+00:00
layout: post
title:  日志·Log(Timestamp+data)
categories: tech
---

> Log = Timestamp + Data.

自工作以来，每每遇到生产环境的问题都不得不践踏傲娇的灵魂，然后默默的去观察日志。生产环境上采用`小黄鸭调试法`显然不奏效，只能事后分析日志，然后采取措施。何不把这个工作持续进行下来，即便线上没有问题，通过日志分析也可提早发现潜在问题，持续优化。

Intro
-----

* [logstash](http://logstash.net)
* [elsticsearch](https://www.elastic.co/products/elasticsearch)
* [kibana](https://www.elastic.co/products/kibana)

一睹为快

Github
------
* [logstash](https://github.com/elastic/logstash)
* [elsticsearch](https://github.com/elastic/elasticsearch) store and index log
* [kibana](https://github.com/elastic/kibana) web fronted

> Using Elasticsearch as a backend datastore, and kibana as a frontend reporting tool, Logstash acts as the workhorse, creating a powerful pipeline for storing, querying and analyzing your logs. With an arsenal of built-in inputs, filters, codecs and outputs, you can harness some powerful functionality with a small amount of effort. 


