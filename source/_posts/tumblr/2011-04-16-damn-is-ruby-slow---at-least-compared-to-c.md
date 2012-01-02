--- 
layout: post
title: damn is ruby slow - at least compared to c++
categories: 
- tumblr
- c++
- ruby
- speed
date: 2011-04-16
---
ok thats nothing new, yet the difference was a little bit surprising.

In an earlier post I described the _puzzleSolver_ project and before starting
to implement parts of it in c++ I build a Ruby prototype. The prototype
generated 1000 random puzzle pieces and later generated a quality between
every 4000 puzzle edges, thats about 8.000.000 calculations. The Ruby
Prototype needs **3 minutes** to finish that calculation.

<!-- more -->

The c++ version does exactly the same, it has the same structure and
algorithm. Now the calculations are done in **under 1 second** for 1000
pieces.

As I sad, its not surprising that the c++ version is way faster than the Ruby
prototype. But a difference of **200 times faster** was surprising.

But I don't want to make Ruby bad, I love Ruby, without the prototype it would
have been way more difficult to build the c++ version. And of cause the time
building the two versions where different, the Ruby prototype was working
within a few hours, plus another few to optimize the algorithm. The c++
version toke a few days till it was working like the prototype, but that might
also had to do that my last c++ encounter was like two years ago. But even so
I just had to re implement the existing algorithm. Without that it would have
taken even longer.

