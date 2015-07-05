---
author: Albert
date: 2015-07-05
layout: post
title: Cassandra(三):面向查询建模
categories: tech
---

>  Cassandra data modeling focuses on the queries. 

Cassandra's data model is a partitioned row store with tunable consistency. Rows are organized into tables; the first component of a table's primary key is the partition key; within a partition, rows are clustered by the remaining columns of the key. Other columns can be indexed separately from the primary key. Because Cassandra is a distributed database, efficiency is gained for reads and writes when data is grouped together on nodes by partition. The fewer partitions that must be queried to get an answer to a question, the faster the response.
