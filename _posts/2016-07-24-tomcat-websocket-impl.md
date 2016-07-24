---
layout: post
title:  Tomcat Webscoket 实现
author: Albert
date:   2016-07-24 12:30:35
categories: tech
---

以tomcat的实现来熟悉java-websocket的规范。

## 一.初始流程

### 1. 基于[SPI机制](https://docs.oracle.com/javase/tutorial/sound/SPI-intro.html)初始化 

> WebSocket Servlet Container Initializer (简称`WsSci`)
>
> ServletContainerInitializers (SCIs) are registered via an entry in the file META-INF/services/javax.servlet.ServletContainerInitializer that must be included in the JAR file that contains the SCI implementation

tomcat-websocket-8.0.36.jar 包中的`org.apache.tomcat.websocket.server.WsSci` 遵循Servlet 3.0标准，并在META-INF/services/javax.servlet.ServletContainerInitializer文件中被指定，此机制即Java中的[SPI机制](https://docs.oracle.com/javase/tutorial/sound/SPI-intro.html)。

### 2.创建WsServerContainer

上一步中最重要的一环为构造并配置了WsServerContainer.

