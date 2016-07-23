---
layout: post
title:  Java WebSocket ｀小样儿｀
author: Albert
date:   2016-07-23 15:30:35
categories: tech
---

`WebSocket`为IM通讯提供了另一种实现方式。

## 一. 环境说明

* JDK 1.7.80
* Tomcat 8.0.36
* Eclipse 4.6.0 

### 1. 按部就班

#### 1. 新建一个Maven Project

#### 2. 添加tomcat-websocket依赖

```xml
<dependency>
	<groupId>org.apache.tomcat</groupId>
	<artifactId>tomcat-websocket</artifactId>
	<version>8.0.36</version>
	<scope>provided</scope>
</dependency>
```

#### 3.其它配置

> 大意就是用JDK1.7编译，war包忽略web.xml文件。

```xml
<build>
	<plugins>
		<plugin>
			<groupId>org.apache.maven.plugins</groupId>
			<artifactId>maven-compiler-plugin</artifactId>
			<configuration>
				<source>1.7</source>
				<target>1.7</target>
				<encoding>UTF-8</encoding>
			</configuration>
		</plugin>
		<plugin>
			<groupId>org.apache.maven.plugins</groupId>
			<artifactId>maven-war-plugin</artifactId>
			<configuration>
				<failOnMissingWebXml>false</failOnMissingWebXml>
			</configuration>
		</plugin>
	</plugins>
</build>
```

### 2.进入正题

```sh
➜  java-websocket tree
.
├── pom.xml
└── src
    ├── main
    │   ├── java
    │   │   └── im
    │   │       └── unx
    │   │           └── java
    │   │               └── websocket
    │   │                   ├── EchoServer.java
    │   │                   ├── ProgrammaticEchoServer.java
    │   │                   └── ProgrammaticEchoServerAppConfig.java
    │   ├── resources
    │   └── webapp
    └── test
        ├── java
        └── resources
```

两种实现：EchoServer基于注解，ProgrammaticEchoServer采用编程式实现。

#### A.基于注解

```JAVA
package im.unx.java.websocket;

import javax.websocket.OnMessage;
import javax.websocket.server.ServerEndpoint;

@ServerEndpoint("/echo")
public class EchoServer {

	@OnMessage
	public String echo(String message) {
		return "Got a message (" + message + ") from the future. Good luck !";
	}

}
```

#### B.编程式实现

```java
package im.unx.java.websocket;

import java.io.IOException;

import javax.websocket.Endpoint;
import javax.websocket.EndpointConfig;
import javax.websocket.MessageHandler;
import javax.websocket.Session;

/**
 * 编程式的实现可以了解更多细节。
 */
public class ProgrammaticEchoServer extends Endpoint {

	@Override
	public void onOpen(Session session, EndpointConfig endpointConfig) {
		final Session mySession = session;
		String queryString = mySession.getQueryString();
		// 可以考虑 token 和session验证通过则进行通讯，否则无法继续。
		System.out.println(queryString);

		mySession.addMessageHandler(new MessageHandler.Whole<String>() {
			@Override
			public void onMessage(String text) {
				try {
					mySession.getBasicRemote().sendText("Got a message (" + text + ") from the future. Good luck !");
				} catch (IOException ioe) {
					System.out.println("something went wrong");
				}
			}
		});
	}

}
```

编程式提供服务端点需要实现ServerApplicationConfig

```java
package im.unx.java.websocket;

import java.util.HashSet;
import java.util.Set;

import javax.websocket.Endpoint;
import javax.websocket.server.ServerApplicationConfig;
import javax.websocket.server.ServerEndpointConfig;

public class ProgrammaticEchoServerAppConfig implements ServerApplicationConfig {

	@Override
	public Set<ServerEndpointConfig> getEndpointConfigs(Set<Class<? extends Endpoint>> scanned) {

		Set<ServerEndpointConfig> configs = new HashSet<ServerEndpointConfig>();

		ServerEndpointConfig sec = ServerEndpointConfig.Builder
				.create(ProgrammaticEchoServer.class, "/echo2").build();

		configs.add(sec);

		return configs;
	}

	@Override
	public Set<Class<?>> getAnnotatedEndpointClasses(Set<Class<?>> scanned) {
		return scanned;
	}

}
```

## 二. 运行调试

1. 部署到tomcat下，启动
2. 编写html
3. 服务端点
   * http://localhost:8080/java-websocket/echo
   * http://localhost:8080/java-websocket/echo2

测试html代码

```html
 <!DOCTYPE html>
<html lang="en">
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Web Socket JavaScript Echo Client</title>
    <script language="javascript" type="text/javascript">
    var echo_websocket;
    function init() {
        output = document.getElementById("output");
    }
    function send_echo() {
        var wsUri = "ws://localhost:8080/java-websocket/echo";
        writeToScreen("Connecting to " + wsUri);
        echo_websocket = new WebSocket(wsUri);
        echo_websocket.onopen = function (evt) {
            writeToScreen("Connected !");
            doSend(textID.value);
        };
        echo_websocket.onmessage = function (evt) {
            writeToScreen("Received message: " + evt.data);
            echo_websocket.close();
        };
        echo_websocket.onerror = function (evt) {
            writeToScreen('<span style="color: red;">ERROR:</span> '
                + evt.data);
            echo_websocket.close();
        };
    }
    function doSend(message) {
        echo_websocket.send(message);
        writeToScreen("Sent message: " + message);
    }
    function writeToScreen(message) {
        var pre = document.createElement("p");
        pre.style.wordWrap = "break-word";
        pre.innerHTML = message;
        output.appendChild(pre);
    }
    window.addEventListener("load", init, false);
    </script>
</head>
<body>
    <h1>Echo Server</h1>
    <div style="text-align: left;">
        <form action="">
            <input onclick="send_echo()" value="Press to send"
            type="button">
            <input id="textID" name="message" value="Hello Web Sockets"
            type="text">
            <br> </form>
        </div>
        <div id="output"></div>
    </body>
</html> 
```

浏览器直接运行即可。

## 三.关于WebSocket其它优势

1. 不存在解决跨域的问题
2. 全双工
3. 协议扩展性比较高，说到底TCP之上需自己实现应用协议。



