--- 
layout: post
title: 'compiling ruby 1.8.7 with gcc 4.6.*'
categories: 
- tumblr
- ruby
- ree
- gcc
date: 2011-09-09
---
the last few days I reinstalled archlinux and encountered a problem. **You
can't compile ruby 1.8.7 or REE 1.8.7 with gcc4.6**. Earlier versions probably
have the same issue, but at least 1.9.2 or newer works.

But I wanted ree installed because its load requirements faster than the newer
build which is important when developing rails.

<!-- more -->

After some googling I just grabbed the source from github and compiled it
myself without relying on the default installer.

You will get 2 errors but they basically the same. While building ruby at some
point two files get generated `callback.func` and `cbtables.func`.
Unfortunately later on exactly these two files are wrong…

The - when you know what to do - easy solution is the following

``` sh
cd ext/dl
rm callback.func cbtables.func
touch callback.func cbtables.func

ruby mkcallback.rb >> callback.func
ruby mkcbtables.rb >> cbtables.func
```

After this go back to the root source folder and run `make` again. Make will
start at the position of the last error, use the new files and finish
building.

