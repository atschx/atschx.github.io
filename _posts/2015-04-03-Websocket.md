---
author: Albert
date: 2015-04-03 23:33:23+00:00
layout: post
title: WebSocket·Notes
categories: tech
---

> 一名coder写代码是本能，用文字记住走过的路 —— 这世界我来过。就此刻·深夜，空气冷却下来...

Here We GO
----------

1. 介绍:Intro Websocket
2. 剖析:I‘m a programmer,not only
3. 落地:In Action

Intro Websocket
===============

websocket没听过，不打紧。反转ajax呢？那些年server端调用前段ajax代码时的各种酸爽，还记得吗(内存爆仓没有)？一起回忆下：

* [commet](http://www.ibm.com/developerworks/cn/web/wa-reverseajax1/)
* [websocket](http://www.ibm.com/developerworks/cn/web/wa-reverseajax2/)

> The WebSocket Protocol enables two-way communication between a client
 running untrusted code in a controlled environment to a remote host
 that has opted-in to communications from that code. The security
 model used for this is the origin-based security model commonly used
 by web browsers. The protocol consists of an opening handshake
 followed by basic message framing, layered over TCP. The goal of
 this technology is to provide a mechanism for browser-based
 applications that need two-way communication with servers that does
 not rely on opening multiple HTTP connections (e.g., using
 XMLHttpRequest or <iframe>s and long polling).

I'm a programmer, not only
==========================

惊鸿一瞥,帅到没朋友~

{% highlight java linenos %}
package com.atschx.summer.websocket;

import javax.servlet.annotation.WebServlet;
import javax.websocket.OnMessage;
import javax.websocket.server.ServerEndpoint;

@WebServlet
@ServerEndpoint("/echo")
public class EchoServer {
	@OnMessage
	public String handleMessage(String message) {
		return "Got your message (" + message + "). Thanks !";
	}
}
{% endhighlight %}

client 代码看这里 [using_websocket_in_javascript_client](http://enterprisewebbook.com/ch8_websockets.html#ex_using_websocket_in_javascript_client)

you know,spec.

 * [rfc6455](http://tools.ietf.org/pdf/rfc6455.pdf)
 * [jsr356](https://jcp.org/en/jsr/detail?id=356)
 * [websocket](http://www.w3.org/TR/websockets/)

读完上面的协议，websocket的建立需要以下几个步骤：

1. 客户端发起Get请求

{% highlight sh linenos %}	
GET ws://localhost:8080/summer-websocket/echo HTTP/1.1
Host: localhost:8080
Connection: Upgrade
Pragma: no-cache
Cache-Control: no-cache
Upgrade: websocket
Origin: http://localhost:8080
Sec-WebSocket-Version: 13
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/40.0.2214.115 Safari/537.36
Accept-Encoding: gzip, deflate, sdch
Accept-Language: zh-CN,zh;q=0.8,en;q=0.6
Sec-WebSocket-Key: w6/VMRsKAqt4CdncJXjKpw==
Sec-WebSocket-Extensions: permessage-deflate; client_max_window_bits
{% endhighlight %}

2. 服务端响应

{% highlight sh linenos %} 
HTTP/1.1 101 Switching Protocols
Server: Apache-Coyote/1.1
Upgrade: websocket
Connection: upgrade
Sec-WebSocket-Accept: x9zpAgi0XqA0u36+nALpK7I4ODw=
Sec-WebSocket-Extensions: permessage-deflate;client_max_window_bits=15
Date: Mon, 27 Apr 2015 17:44:52 GMT
{% endhighlight %}

备注：通过指定的`Upgrade: websocket` [请求协议升级websocket](https://tools.ietf.org/html/rfc6455#section-11.2),理所应当的这条请求的Connection为upgrade.Sec-打头的几个需要特别关注下，这个也将涉及到安全策略问题。

> 在`ajax`的世界里，跨域访问的安全问题就受限于同源策略，websocket从协议设计层面化解了同源的爱恨情仇。

延伸阅读

* [通用首部](http://en.wikipedia.org/wiki/List_of_HTTP_header_fields#Request_fields)
* [connection](http://tools.ietf.org/html/rfc7230#section-6.1)
* [upgrade](http://en.wikipedia.org/wiki/HTTP/1.1_Upgrade_header)
* [BuildingHTML5WebSocketApplicationsInJava](https://qconsf.com/sf2012/dl/qcon-sanfran-2012/slides/ArunGupta_JSR356BuildingHTML5WebSocketApplicationsInJavaMOVEDTOSEACLIFFAB.pdf)

In Action
=========

> Websocket在生产环境中落地，思考应用层安全问题

![Websocket Sec]({{ site.baseurl }}/assets/images/2015/04/websoket-sec-cables.jpg)

* [developer.kaazing](http://developer.kaazing.com/documentation/html5/3.5/security/c_sec_security.html)
* [html5-websocket-security](http://blog.kaazing.com/2012/02/28/html5-websocket-security-is-strong/)
* [html5-websocket-gateway-security](http://blog.kaazing.com/2012/02/29/kaazing-websocket-gateway-security-is-strong/)


The WebSocket protocol uses the 400 Bad Request HTTP error code to signal an unsuccessful upgrade
[Upgrading HTTP to WebSocket](http://enterprisewebbook.com/ch8_websockets.html)

Load Balance
------------

![haproxy-websocket]({{ site.baseurl }}/assets/images/tech/haproxy_websocket.png)

[haproxy-websocket](http://blog.haproxy.com/2012/11/07/websockets-load-balancing-with-haproxy/)

> [HTML5定稿](http://www.w3.org/TR/html5/)，`websocket`一骑绝尘，`cavas`风情万种，liveApp遍地开花......
