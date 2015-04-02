---
author: Albert
date: 2014-03-13 15:58:29+00:00
layout: post
title: JavaFX中Platform.runlater和Task
wordpress_id: 227
categories: JavaFX
tags: JavaFX
---

在JavaFX编程中，什么情况下该用Platform.runlater(..)什么时候用Task，对于刚上手JavaFX的同学来说都很模糊，请记住两条即可。

  * 需要在GUI**线程之外更新UI时**请考虑Platform.runlater(..)
  * 为避免GUI线程卡死执行长时间操作时请使用Task

参见：[http://stackoverflow.com/questions/13351959/javafx-how-to-set-default-active-control/13352107#13352107](http://stackoverflow.com/questions/13351959/javafx-how-to-set-default-active-control/13352107#13352107)
