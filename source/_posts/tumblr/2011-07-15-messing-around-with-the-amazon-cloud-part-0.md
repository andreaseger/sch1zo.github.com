--- 
layout: post
title: Messing around with the Amazon Cloud Part 0
categories: 
- tumblr
- amazon
- amazon web services
- aws
- cloud
date: 2011-07-15
---
so out of curiosity I just registered for [Amazon Web
Services](http://aws.amazon.com/) and my plan is to just use the free tier
Amazon provides [link](http://aws.amazon.com/free).

<!-- more -->

Right now after about half an hour I have my first micro instance up and it
runs [Amazon Linux (Beta)](http://aws.amazon.com/amazon-linux-ami/). Thats a
maintained and supported Linux image which just fits in the free tier plan. As
far as I can tell it has its background in the Red Hat camp and uses yum as
package manager.

The Management Console is at first glance is nice but you definitely have to
get the hang of it. There's many stuff to configure and setup, but more on
that later.

First downer: I couldn't get the Archlinux images running, will have to look
into that at some point.

Another weird thing is that once you are in the management console your not
really have control over your costs, but at least when you create a new
instance it will show you if it will fit in the free plan.

Next Steps are

  * install zsh, vim, screen, ruby - rvm
  * make the necessary setup for the above (basically import my rc files)
  * watch how the micro instance performs

