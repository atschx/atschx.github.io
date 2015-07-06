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

<pre>
[sunchanghao@vm_10_119 cassandra]$ bin/nodetool cfstats statistic.protocols_order_by_bytes
Keyspace: statistic
	Read Count: 12
	Read Latency: 1.9284166666666667 ms.
	Write Count: 7485502
	Write Latency: 0.018335492796608698 ms.
	Pending Flushes: 0
		Table: protocols_order_by_bytes
		SSTable count: 3
		Space used (live): 3271427
		Space used (total): 3271427
		Space used by snapshots (total): 0
		Off heap memory used (total): 1346
		SSTable Compression Ratio: 0.3192803109235681
		Number of keys (estimate): 3
		Memtable cell count: 4179439
		Memtable data size: 1699798
		Memtable off heap memory used: 0
		Memtable switch count: 3
		Local read count: 12
		Local read latency: 1.929 ms
		Local write count: 7485539
		Local write latency: 0.019 ms
		Pending flushes: 0
		Bloom filter false positives: 0
		Bloom filter false ratio: 0.00000
		Bloom filter space used: 48
		Bloom filter off heap memory used: 24
		Index summary off heap memory used: 66
		Compression metadata off heap memory used: 1256
		Compacted partition minimum bytes: 943128
		Compacted partition maximum bytes: 3379391
		Compacted partition mean bytes: 2676673
		Average live cells per slice (last five minutes): 30.166666666666668
		Maximum live cells per slice (last five minutes): 51.0
		Average tombstones per slice (last five minutes): 0.0
		Maximum tombstones per slice (last five minutes): 0.0

----------------
</pre>

