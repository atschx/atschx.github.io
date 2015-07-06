---
author: Albert
date: 2015-07-05
layout: post
title: Cassandra(三):面向查询建模
categories: tech
---

>  Cassandra data modeling focuses on the queries. 

Cassandra's data model is a partitioned row store with tunable consistency. Rows are organized into tables; the first component of a table's primary key is the partition key; within a partition, rows are clustered by the remaining columns of the key. Other columns can be indexed separately from the primary key. Because Cassandra is a distributed database, efficiency is gained for reads and writes when data is grouped together on nodes by partition. The fewer partitions that must be queried to get an answer to a question, the faster the response.

**按报文字节大小查询**

>说明: 主键部分基于日期进行分区存储,按字节大小降序 

<pre>
CREATE TABLE statistic.protocols_order_by_bytes (
	occured_on text,
	bytes int,
	channel int,
	client_type int,
	client_version text,
	ip_address text,
	occured_at timestamp,
	seq int,
	sid bigint,
	tag int,
	type int,
	uid int,
	PRIMARY KEY (occured_on, bytes)
) WITH CLUSTERING ORDER BY (bytes DESC)
</pre>
