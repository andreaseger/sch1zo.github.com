--- 
layout: post
title: Messing around with the Amazon Cloud Part 1
categories: 
- tumblr
- amazon
- amazon web services
- cloud
- aws
date: 2011-07-15
---
after getting the EC2 Instance up and running its time to install a basic
development environment.

  * zsh and screen makes as expected no problems.
  * vim is unfortunately not compiled with ruby and I couldn't find another one in the repository so it has to work without it
  * rvm again no problem. As I'm writing this post ruby 1.9.2 is compiling, which given the power of a micro instance is slow perhaps to slow to do anything with it, but time will see.

<!-- more -->

Next time setting up such a machine it may be no bad idea to get a bigger
instance for a few hours, just to make the compiling faster.

What surprised me was how minimal the installed linux were, no unnecessary
packages just the stuff I want.

Next steps:

  * compiling nginx (with passenger) - this could take a while given the speed of the instance
  * running a few of my small sinatra and rails apps
  * will this instance be fast enough to do development?

