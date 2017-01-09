---
layout: post
title:  macOS install ffmpeg 备注
author: Albert
date:   2017-01-09 23:43:30
categories: tech
---

> `ffmpeg`处理视频,`ffplay`是`ffmpeg`为测试其`codec lib`而开发的基于命令行的播放器。

直接查看install  log 备注

```bash
➜  ~ brew install ffmpeg --with-ffplay
Updating Homebrew...
==> Auto-updated Homebrew!
Updated 1 tap (homebrew/core).
==> Updated Formulae
aubio               go                  h2o                 leptonica           libtiff             nexus               pbzip2              pod2man             vim
git-test            godep               icoutils            lft                 mikutter            nim                 pcsc-lite           vice

==> Installing dependencies for ffmpeg: gettext, texi2html, yasm, lame, x264, xvid, sdl2
==> Installing ffmpeg dependency: gettext
==> Downloading https://homebrew.bintray.com/bottles/gettext-0.19.8.1.sierra.bottle.tar.gz
######################################################################## 100.0%
==> Pouring gettext-0.19.8.1.sierra.bottle.tar.gz
==> Caveats
This formula is keg-only, which means it was not symlinked into /usr/local.

macOS provides the BSD gettext library and some software gets confused if both are in the library path.

Generally there are no consequences of this for you. If you build your
own software and it requires this formula, you'll need to add to your
build variables:

    LDFLAGS:  -L/usr/local/opt/gettext/lib
    CPPFLAGS: -I/usr/local/opt/gettext/include

==> Summary
🍺  /usr/local/Cellar/gettext/0.19.8.1: 1,934 files, 16.9M
==> Installing ffmpeg dependency: texi2html
==> Downloading https://homebrew.bintray.com/bottles/texi2html-5.0.sierra.bottle.tar.gz
######################################################################## 100.0%
==> Pouring texi2html-5.0.sierra.bottle.tar.gz
🍺  /usr/local/Cellar/texi2html/5.0: 278 files, 6.2M
==> Installing ffmpeg dependency: yasm
==> Downloading https://homebrew.bintray.com/bottles/yasm-1.3.0.sierra.bottle.2.tar.gz
######################################################################## 100.0%
==> Pouring yasm-1.3.0.sierra.bottle.2.tar.gz
🍺  /usr/local/Cellar/yasm/1.3.0: 44 files, 3.1M
==> Installing ffmpeg dependency: lame
==> Downloading https://homebrew.bintray.com/bottles/lame-3.99.5.sierra.bottle.1.tar.gz
######################################################################## 100.0%
==> Pouring lame-3.99.5.sierra.bottle.1.tar.gz
🍺  /usr/local/Cellar/lame/3.99.5: 26 files, 2M
==> Installing ffmpeg dependency: x264
==> Downloading https://homebrew.bintray.com/bottles/x264-r2728.sierra.bottle.tar.gz
######################################################################## 100.0%
==> Pouring x264-r2728.sierra.bottle.tar.gz
🍺  /usr/local/Cellar/x264/r2728: 11 files, 3.3M
==> Installing ffmpeg dependency: xvid
==> Downloading https://homebrew.bintray.com/bottles/xvid-1.3.4.sierra.bottle.tar.gz
######################################################################## 100.0%
==> Pouring xvid-1.3.4.sierra.bottle.tar.gz
🍺  /usr/local/Cellar/xvid/1.3.4: 9 files, 1.2M
==> Installing ffmpeg dependency: sdl2
==> Downloading https://homebrew.bintray.com/bottles/sdl2-2.0.5.sierra.bottle.tar.gz
######################################################################## 100.0%
==> Pouring sdl2-2.0.5.sierra.bottle.tar.gz
🍺  /usr/local/Cellar/sdl2/2.0.5: 84 files, 4.0M
Warning: ffmpeg: --with-ffplay was deprecated; using --with-sdl2 instead!
==> Installing ffmpeg --with-sdl2
==> Using the sandbox
==> Downloading https://ffmpeg.org/releases/ffmpeg-3.2.2.tar.bz2
######################################################################## 100.0%
==> ./configure --prefix=/usr/local/Cellar/ffmpeg/3.2.2 --enable-shared --enable-pthreads --enable-gpl --enable-version3 --enable-hardcoded-tables --enable-avresample --cc=clang --h
==> make install
🍺  /usr/local/Cellar/ffmpeg/3.2.2: 244 files, 52.3M, built in 2 minutes 56 seconds
```