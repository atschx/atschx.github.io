---
author: Albert
date: 2015-01-24 14:31:09+00:00
layout: post
title: ZooKeeper Cluster (AWS)
categories: aws zookeeper
tags: aws zookeeper
---

> 开篇，总想唠叨一下
	
  1. 2011年，亚马逊在中国不叫亚马逊，卓越网，还记得吗？
  2. 2012年，在amazon.com海淘$119.0抢购kindle，几经波折到手中。
  3. 2013年，z.cn成为我脑海浮现出的首选购书网站
  4. 2014年，alibaba上市，阿里云中国崛起（借本地化红利），亚马逊云入驻中国
		* 天时、地利、人和
		* 好戏开始了....
  5. 2015年，我在aws上搭建了zookeeper集群

# AWS EC2

第一次接触AWS是在2012年，培养了我对弹性计算，按需收费的认识，觉得很坑，典型的企业型操作界面不实用，果断选择linode。倒是"云计算"从09年炒作，到现在IT才算落地，也算对昔日有所交代。

## 准备
	
  * 亚马逊帐号
  * 一张双币信用卡

## 开拨

注册，绑定信用卡，扣$1.0，Launch Instance 一步步开始走进属于你的aws世界
	
  1. Launch EC2 instance
  2. Choose an Amazon Machine Image（选个free的AMI,eg:ubuntu 14.04）
  3. Choose an Instance Type(t2.micro free only)
  4. Configure Instance Details(默认VPC，选个子网，IP Auto Assgin)
  5. Add Storge（root->/dev/sda1->10G，不附加其他卷）
  6. Configure Security Group(ps:all traffic source anywhere )
  7. Edit tag(最好标记下这个实例干什么用的,方便管理，本例ZooKeeper)
  8. Review Instance Launch ->**Launch**

别忘了生成keypair，实例Launch 成功之后，ssh -i keypair 'user@pubic ip'


## ZooKeeper

  1. Download and install jdk 1.6(jdk6普及率远胜于jdk7)
  2. Download zookeeper 3.4.6

简单粗暴上代码，对于任何技术或者语言的学习，实战胜于千言.

step 1:
    
    #install jdk
    cp jdk-6u29-linux-x64.bin /usr/local/
    cd /usr/local 
    chmod u+x  jdk-6u29-linux-x64.bin
    sudo -s ./ jdk-6u29-linux-x64.bin
    ln -s jdk1.6.0_29/ jdk
    
    sudo vi /etc/profile
    
    # configure java 
    export JAVA_HOME=/usr/local/jdk
    export JRE_HOME=$JAVA_HOME/jre
    export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib:$CLASSPATH
    export PATH=.:$JAVA_HOME/bin:$PATH
    
    #make it work
    sudo source /etc/profile


step 2 ：
    
    #configure zookeeper
    wget http://mirrors.gigenet.com/apache/zookeeper/zookeeper-3.4.6/zookeeper-3.4.6.tar.gz
    cp zookeeper-3.4.6.tar.gz /usr/local/
    cd /usr/local/
    tar zxvf zookeeper-3.4.6.tar.gz
    ln -s zookeeper-3.4.6/ zookeeper
    mkdir -p zookeeper/data/
    cp zookeeper/conf/zoo_sample.cfg zookeeper/conf/zoo.cfg
    cd zookeeper && ./bin/zkServer.sh start


step 3：test
    
    #......省略log部分
    [ec2-user@ip-172-31-23-30 zookeeper]$ bin/zkCli.sh
    [zk: localhost:2181(CONNECTED) 0]
    [zk: localhost:2181(CONNECTED) 0] ls /
    [zookeeper]
    [zk: localhost:2181(CONNECTED) 1] create /zk_test atschx
    Created /zk_test
    [zk: localhost:2181(CONNECTED) 2] get /zk_test
    atschx
    cZxid = 0x6
    ctime = Sat Jan 24 23:28:56 EST 2015
    mZxid = 0x6
    mtime = Sat Jan 24 23:28:56 EST 2015
    pZxid = 0x6
    cversion = 0
    dataVersion = 0
    aclVersion = 0
    ephemeralOwner = 0x0
    dataLength = 6
    numChildren = 0
    [zk: localhost:2181(CONNECTED) 3] ls /
    [zookeeper, zk_test]
    [zk: localhost:2181(CONNECTED) 4]

至此，zookeeper单实例安装也就完成了。


## Cluster Install ZooKeeper

AWS的优势在这里可谓是表现的淋漓尽致，小伙伴们都惊呆了....

[![aws_create_ami](http://www.atschx.com/wp-content/uploads/2015/01/aws_create_ami.png)](http://www.atschx.com/wp-content/uploads/2015/01/aws_create_ami.png)你可以采用 Launch More Like This的方式直接复制配置启动一个新的实例，jdk环境，zookeeper环境需要再按照上面的步骤安装配置一遍。除此之外，也可以采用如图中标注的方式打包你的EC2实例，这个来的痛快。总之，继续下面的步骤之前你要再运行两个EC2实例。

> 集群配置

### IP规划

  * 172.31.23.30
  * 172.31.23.31
  * 172.31.23.32

### zoo.cfg
    
    # The number of milliseconds of each tick
    tickTime=2000
    # The number of ticks that the initial 
    # synchronization phase can take
    initLimit=10
    # The number of ticks that can pass between 
    # sending a request and getting an acknowledgement
    syncLimit=5
    # the directory where the snapshot is stored.
    # do not use /tmp for storage, /tmp here is just 
    # example sakes.
    dataDir=/usr/local/zookeeper/data
    # the port at which the clients will connect
    clientPort=2181
    
    server.1=172.31.23.30:2888:3888
    server.2=172.31.23.31:2888:3888
    server.3=172.31.23.32:2888:3888
    # the maximum number of client connections.
    # increase this if you need to handle more clients
    #maxClientCnxns=60
    #
    # Be sure to read the maintenance section of the 
    # administrator guide before turning on autopurge.
    #
    # http://zookeeper.apache.org/doc/current/zookeeperAdmin.html#sc_maintenance
    #
    # The number of snapshots to retain in dataDir
    #autopurge.snapRetainCount=3
    # Purge task interval in hours
    # Set to "0" to disable auto purge feature
    #autopurge.purgeInterval=1

###  myid

每个server的 /usr/local/zookeeper/data 目录下创建myid文件，写入server的id号.
    
    cd /usr/local/zookeeper/data
    touch myid
    echo 1 > myid

依次启动zookeeper，测试下吧.

> 备注：测试完记得stop EC2实例，不要给别人留下扣费的理由。

12年初识亚马逊云时感觉console及其不专业，典型的企业型管理类web系统风格（每曾想它背后所做的事情）。13年购置第一台linode主机后嗷嗷的下载速度为平时工作带来更精彩的便利（youtube&viemo上的技术视频,slideshare技术大拿的分享）。随着2014年google被中国彻底墙掉，linode俨然成了很重要的一个跳板...
