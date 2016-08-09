---
layout: post
title:  MAC下使用 curl+nghttp2 测试APNs
author: Albert
date:   2016-08-08 23:30:35
categories: tech
---

> 备注: 用于后续调试

## 上干货

1. p12证书转换为pem
2. curl 是否支持http2
3.  参考[APNs Provider API](https://developer.apple.com/library/prerelease/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/APNsProviderAPI.html#//apple_ref/doc/uid/TP40008194-CH101-SW1)

```bash
./curl -i --http2 \
-E /tmp/aps_starred.pem \
-d '{"aps":{"alert":"datapacket aha..","badge":1,"sound":"push.caf"}}' \
-H 'Content-Type: application/json; charset=UTF-8' \
-H 'apns-topic:im.cia.Starred' \
"https://api.development.push.apple.com/3/device/7df0cc3e04dbe0208491511df7b4b0f1f915ca6d9550f351d6a12e81a158b15f" 
```

**注意** `apns-topic ` 需要根据证书情况来：

* If your certificate includes multiple topics, you must specify a value for this header.
* If you omit this header and your APNs certificate does not specify multiple topics, the APNs server uses the certificate’s Subject as the default topic.

## 细节看这里

1. mac 上升级curl 并启用支持 http2

```bash
brew install curl --with-nghttp2
```

2. 开发导出的p12证书转为pem

```bash
openssl pkcs12 -in aps_demo.p12 -out aps_demo.pem -nodes -clcerts
```