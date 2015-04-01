---
author: Albert
date: 2015-01-19 16:45:16+00:00
layout: post
title: mysql(percona)
categories: mysql
tags: linux mysql
---

## percona-server


参阅：[percona 官方apt-repo安装说明文档](http://www.percona.com/doc/percona-server/5.6/installation/apt_repo.html)

  1. apt-key adv --keyserver keys.gnupg.net --recv-keys 1C4CBDCDCD2EFD2A
  2. vi /etc/apt/sources.list

	deb http://repo.percona.com/apt trusty main
	deb-src http://repo.percona.com/apt trusty main

  3. apt-get update
  4. apt-get install percona-server-server-5.6 percona-server-client-5.6

安装过程中，设置root密码，done.

> PS：Ubuntu 14.04.1 LTS(trusty)

  * [sakila database](http://dev.mysql.com/doc/sakila/en/index.html)
  * [employee data](https://launchpad.net/test-db/employees-db-1/1.0.6/+download/employees_db-full-1.0.6.tar.bz2)



