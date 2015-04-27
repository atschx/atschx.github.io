---
author: Albert
date: 2015-04-03 23:33:23+00:00
layout: post
title: WebSocket·Notes
categories: tech
---

> [HTML5定稿](http://www.w3.org/TR/html5/)，`websocket`一骑绝尘，`cavas`风情万种，liveApp遍地开花......

作为一名coder安静地写代码是本能，记住走过的路 —— 这世界我来过。就此刻空气冷却下来，深夜...

Here We GO
----------

1. 介绍：websocket
2. 案例：step by step
3. 思考：碎碎念

Intro Websocket
===============

websocket没听过，不打紧。反转ajax呢？那些年server端调用前段ajax代码时的各种酸爽，内存/网络/会话/轮询 etc.

* [commet](http://www.ibm.com/developerworks/cn/web/wa-reverseajax1/)
* [websocket](http://www.ibm.com/developerworks/cn/web/wa-reverseajax2/)

Security
--------

> Websocket在生产环境中落地后，开始思考应用层安全问题。

在ajax的世界中我们经常面临跨域访问的问题，受限于同源策略。websocket从协议设计层面化解了同源的爱恨情仇。
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

