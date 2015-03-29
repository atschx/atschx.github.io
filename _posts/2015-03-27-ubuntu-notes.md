---
layout: post
title:  "Ubuntu Notes"
date:   2015-03-28 03:15:35
categories: linux
---
>Linux/Unix change the word.

##输入法

不吐槽任何一种输入法框架，基本归于两类ibus和fcitx。ubuntu14.04.1默认安装ibus，倾向切换到fcitx.

{% highlight sh linenos %}

#install fcitx
apt-get install fcitx fcitx-config-gtk fcitx-googlepinyin fcitx-module-cloudpinyin  im-switch
#reinstall control center
apt-get install unity-control-center
#language-support disappeared,who care? try it.
#http://apt.ubuntu.com/p/language-selector-gnome

{% endhighlight %}

##工具链

* ssh/scp
* git 
* wget/curl
* screen
* maven
* jdk
