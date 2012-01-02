--- 
layout: post
title: Standalone autotest
categories: 
- tumblr
- ruby
- autotest
- rspec
- standalone
date: 2011-05-16
---
after setting up rspec here is some code to get autotest working with rspec.

In addition it shows nice notifications on every test run, so you don't even
have to lock in the console window.

You only have to save the following gist as **.autotest**

[edit:] removed the Autotest.add_discovery part from the gist as mentioned in
the comments. Just add a **.rspec** file in the same directory to get autotest
speak RSpec

[Source](http://www.stupididea.com/2009/03/15/non-rails-autotest-rspec-
libnotify-linux/)

