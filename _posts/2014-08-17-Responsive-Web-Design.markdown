---
author: Albert
date: 2014-08-17 15:34:39+00:00
layout: post
title: 响应式WEB设计
categories: tech
tags:
- 响应式
---

几年前，开发前端的小伙伴们一般会选择960这个神奇的数字适配不同分辨率的显示器（主流莫过于1024*768/1366*768/1920*1080）。随着科技的不断发展，一大波儿不同尺寸的移动智能设备向我们涌来，移动端的对WEB设计提出了新的要求，怎么办？

2010年5月25日，Ethan Marcotte(伊桑 马科特)在A List Apart 上发表了一篇文章[《Responsive Web Design》](http://alistapart.com/article/responsive-web-design/)，打开了WEB设计的新思路。

这几年一直在做企业级WEB应用，比较习惯的用法都是改造一些现成的JS前端UI框架，何谈WEB设计。HTML5和CSS3的火热也就没有点燃手上的项目，只是偶尔关注下，耳边关于响应式设计发声最多的有两点：媒体查询和流式布局。

最近客户项目需求中需要开发一个手机办公网站，和WEB设计沾点边，一不做二不休，干脆把响应式WEB设计的理念好好理解下并在项目中贯穿一吧。

先谈媒体查询(Media Queries)，媒体查询是CSS规范的一部分，个人理解其大意是说针对不同尺寸的viewport提供不同的CSS样式，以达到最佳的阅读效果。关于这部分用法可参考：[whats-this-all-about-css-media-queries](http://claricetechnologies.com/blog/2012/12/whats-this-all-about-css-media-queries/)。

[![Clarice-Technologies_CSS](http://www.jfxgraph.com/wp-content/uploads/2014/08/Clarice-Technologies_CSS.png)](http://www.jfxgraph.com/wp-content/uploads/2014/08/Clarice-Technologies_CSS.png)

再谈流式布局：

我记得刚接触HTML时，布置的课后作业是用Table布局去模仿魔兽世界官方的网站，那个时候各种算啊，现在想来还是蛮崇拜那时的自己，为1像素的间隙调来调去。那时候学校里教的是20世纪90年代末的技术，而世面上早已是DIV+CSS+JS 漫天飞的时代，顿时感觉中国的教育真的有点儿让人汗颜。

在这里我们项那些奋战在客户端原生APP领域的小伙伴们致敬：

Andriod 原生APP开发真是一把辛酸一把泪，做个产品容易吗? IOS的小伙伴们相对摆出高逼格的姿态，我们不怕，iPhone，iPad是我们强硬的后台。
