--- 
layout: post
title: how to compile a fast imagemagick
categories: 
- tumblr
- imagemagick
- c++
- gcc
date: 2011-09-06
---
yesterday I had to install [ImageMagick](http://www.imagemagick.com) to do
some image processing on a new webapp I'm building - creating thumbnails of
uploaded images to be precise.

The initial choice was to simply use the the package from the repository. But
it was unbarable slow to simply create a 100x100 thumbnail of a 1080p
wallpaper which I used to test it( time sad a little above 7 seconds).

<!-- more -->

So the logical next step was to get the source and compile ImageMagick by
hand. But I didn't stopped there. After a quick search I found some tips to
get it even faster:

  * first lets mess around with the compiler optimization I found [here](http://wikis.sun.com/display/AppPerfTuning/ImageMagick) but I did not change the CC CXX or CFLAGS instead I only modified CXXFLAGS

export CXXFLAGS = "-g0 -fast -zlazyload"

  * make it use only about half the memory configure with with-quantum-depth=8 instead of the default 16

./configure --with-quantum-depth=8

If this gives you a snappy imagemagick your fine, but on my ubuntu server a
simple resize still took 7 seconds.

So I did a little bit more searching and found out that a buggy OpenMP can
cause this issue and disabling it while compiling fixes the slowness.

**Finally here my complete configure line**

``` sh
./configure CXX="g++" CXXFLAGS="-g0 -fast -zlazyload" --with-quantum-depth=8 --disable-openmp
```

* * *

I know this post is a mess, but I dont care

