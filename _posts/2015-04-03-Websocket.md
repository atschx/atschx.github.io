---
author: Albert
date: 2015-04-03 17:33:10+00:00
layout: post
title: WebSocket·Notes
categories: tech
---

> `html5`标准定稿，`websocket`一骑绝尘，liveApp遍地开花......

关于推送
--------

* [commet](http://www.ibm.com/developerworks/cn/web/wa-reverseajax1/)
* [websocket](http://www.ibm.com/developerworks/cn/web/wa-reverseajax2/)

> 之前称之为反转Ajax.

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

