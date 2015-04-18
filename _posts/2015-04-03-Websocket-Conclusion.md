---
author: Albert
date: 2015-04-03 17:33:10+00:00
layout: post
title: Websocket的几点总结
categories: tech
---

> NB哄哄的`html5`标准在去年定稿之后，websocket就成了web开发中全双工通讯的典范。在ajax的世界中我们经常面临跨域访问的问题，受限于同源策略。websocket从协议设计层面化解了同源的爱恨情仇。

Security
--------

> Websocket在生产环境中落地后，开始思考应用层安全问题。

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

