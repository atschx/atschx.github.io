---
author: Albert
date: 2015-07-04
layout: post
title: Cassandra(一):逼上梁山
categories: tech
---

> [<<IM场景下的系统拓扑及协议优化>>]({{ site.baseurl }}/tech/2015/07/01/im-topology-and-protocol-statistic.html)中留下一个问题:存储交互的每条协议,按大小排序给出Top N ?

首先这个问题其实有两层含义:

1. 如何存 ? (除了高效的写,还要有足够的容量)
2. 排序给出Top N ? (即使样本再大,也要排序给出结果)

最简单的办法:`mysql中创建一张表,order by bytes desc limit N`.这是所有程序员都能想到的`短平快`的办法,**然并卵**.有人说,用Hadoop吧.可目前的需求用Hadoop解决有些小题大作,最后锁定Nosql领域的`Cassandra`.就像这名字一样,清澈而又明亮.[逼上梁山](http://cassandra.apache.org)...

> [cassandra]({{ site.baseurl }}/assets/images/nosql/cassandra/Cassandra_logo.svg.png):“你也是，疯狂也将找上你。”

![cassandra](http://cassandra.apache.org/media/img/cassandra_logo.png)
 
> The Apache Cassandra database is the right choice when you need scalability and high availability without compromising performance. Linear scalability and proven fault-tolerance on commodity hardware or cloud infrastructure make it the perfect platform for mission-critical data. Cassandra's support for replicating across multiple datacenters is best-in-class, providing lower latency for your users and the peace of mind of knowing that you can survive regional outages.

眼前一亮
--------

> 分布式 线性扩展


	package com.atschx.cassandra.sample;
	
	import java.net.InetAddress;
	import java.util.Date;
	import java.util.UUID;
	
	public class IMProtocolStatisticModel {
	
		private UUID id;
	
		private Integer uid;
		private Long sid;
		private InetAddress ipAddress;
		private Date occuredOn;
	
		private Integer seq;
		private Integer channel;
		private Integer tag;
		private Integer type;
		private String packet;
		private Integer bytes;
	
		private String clientVersion;
		private Integer clientType;

		....//省略setter和getter
	}

[本文案例源码](https://github.com/atschx/cassandra-sample)

