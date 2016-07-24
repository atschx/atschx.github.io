---
layout: post
title:  Tomcat Webscoket 实现
author: Albert
date:   2016-07-24 12:30:35
categories: tech
---

以tomcat的实现来熟悉java-websocket的规范。

##一.初始流程

### 1. 通过SPI机制初始化WebSocketServletContainerInitializers(简称`WsSci`)

`org.apache.tomcat.websocket.server.WsSci` 遵循Servlet 3.0标准(ServletContainerInitializers (SCIs) are registered via an entry in the file META-INF/services/javax.servlet.ServletContainerInitializer that must be included in the JAR file that contains the SCI implementation)。

此类在tomcat-websocket-8.0.36.jar包中，并在META-INF/services/javax.servlet.ServletContainerInitializer文件中被指定，此机制为JAVA自身的[SPI机制](https://docs.oracle.com/javase/tutorial/sound/SPI-intro.html)。

