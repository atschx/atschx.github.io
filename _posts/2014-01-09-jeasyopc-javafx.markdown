---
author: Albert
date: 2014-01-09 15:24:26+00:00
layout: post
title: 浅析JEasyOPC与JavaFX
categories:
- tech
tags:
- JEasyOpc
---

OPC工作原理

[![OPCDataAccessArch](http://www.jfxgraph.com/wp-content/uploads/2014/01/OPCDataAccessArch.jpg)](http://www.jfxgraph.com/wp-content/uploads/2014/01/OPCDataAccessArch.jpg)

关于[opcDataAccess](http://itcofe.web.cern.ch/itcofe/Services/OPC/GeneralInformation/Specifications/RelatedDocuments/DASummary/DataAccessOvw.html)。

[![OPCDataAccessModel](http://www.jfxgraph.com/wp-content/uploads/2014/01/OPCDataAccessModel.jpg)](http://www.jfxgraph.com/wp-content/uploads/2014/01/OPCDataAccessModel.jpg)

11年，客户现场部署了一个遗留基于JEasyOPC编写的OPC客户端，其主要功能是接收硬件设备发来的信号，形成命令池，由中控室人员通过此客户在下发具体的硬件操作指令。想想哪会儿，傻乎乎的特别着迷，心中充满了拯救世界的想法。

最近正好再次接触OPC,决定潜心研究一下。

本文以JeasyOpc为主线，穿插介绍其他相关技术.

### 下载源码

[JEasyOPC](http://sourceforge.net/projects/jeasyopc/) :[http://sourceforge.net/projects/jeasyopc/](http://sourceforge.net/projects/jeasyopc/)

下载后目录结构如下：

[![jeasyopc-filelist](http://www.jfxgraph.com/wp-content/uploads/2014/01/jeasyopc-filelist.png)](http://www.jfxgraph.com/wp-content/uploads/2014/01/jeasyopc-filelist.png)

### 环境准备

如果要测试OPC肯定需要OPC模拟设备，推荐使用matrikonopc，关于MartrikonOPC的使用读者可另行Google.此处不再做详细介绍。

### 编写DEMO

  1. **Jopc.coInitialize()**
  2. **new JEasyOpc 实例 --> jopc**
  3. **new OpcGroup 实例-->testGroup**
  4. testGroup.addAsynchListener(OpcAsynchGroupListener的一个实现用于接受异步事件)
  5. new OpcItem 实例（这个随便，可以多整几个）
  6. 将opcItem实例化添加到刚才的testGroup中
  7. 将testGroup添加到JEasyOpc实例中（jopc.addGroup(group)）
  8. **jopc.connect();**
  9. **jopc.start();**

按照上述流程即可完成一个简单Demo.

### 注意问题

**使用JavaFX时，第一步代码的执行要在Application.start()方法之前运行，推荐在init方法中调用.**

有关OPC开发相关的可参考：[http://www.opcconnect.com/](http://www.opcconnect.com/)

相关标准：[http://www.opcfoundation.org/SiteMap.aspx?MID=Downloads](http://www.opcfoundation.org/SiteMap.aspx?MID=Downloads)


