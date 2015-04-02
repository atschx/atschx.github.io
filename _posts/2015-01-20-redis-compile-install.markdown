---
author: Albert
comments: false
date: 2015-01-20 16:39:02+00:00
layout: post
title: Redis compile install
tags: Redis
---

> 准备环境：ubuntu 14.04.1(trusty)

参考资料：

  1. [redis官方指南](http://redis.io/topics/quickstart)
  2. [tcl](http://www.linuxfromscratch.org/blfs/view/cvs/general/tcl.html)

下载redis最新源码包:
    
    wget http://download.redis.io/redis-stable.tar.gz
    tar xvzf redis-stable.tar.gz
    cd redis-stable/src
    make

建议到src目录下运行make，否则需自己解决redis相关依赖库.

make test
You need tcl 8.5 or newer in order to run the Redis test
make: *** [test] Error 1

apt-cache search tcl|grep 8.6
安装tcl之后，执行make test.测试通过，将target文件copy至/usr/local/bin目录下

    sudo cp src/redis-server /usr/local/bin/
    sudo cp src/redis-cli /usr/local/bin/
    #启动redis
    redis-server

客户端test
    
    albert@thinker:~$ redis-cli 
    127.0.0.1:6379> set foo test
    OK
    127.0.0.1:6379> get foo
    "test"
    127.0.0.1:6379>

have fun！
