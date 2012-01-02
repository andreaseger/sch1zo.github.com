--- 
layout: post
title: using my ec2 instance to get a US IP
categories: 
- tumblr
- Amazon Web Services
- aws
- cloud
- ip
- us
- ssh
- vpn
- gema
- youtube
date: 2011-08-12
---
Today I was surfing around and once again I got that ugly GEMA message on a
youtube music video which prevented me from watching it. In the last months
more and more videos got blocked this way and makes having a german IP a pain.

But than I remembered that I can set up a Micro Instance in one of the US
datacentrers and route my web traffic through it.

<!-- more -->

So what are my options to do this?

  * setting up a proxy server on that instance
  * establish a ssh tunnnel and use that as local proxy
  * set up a VPN server on the instance and use that to reroute my traffic

Because I don't like having to set a proxy in each and every browser and app I
have and than always having to keep my tunnel open I decided to look into the
VPN solution. After all I can fall back to the tunnel at any time - for
example if I need to connect to another VPN and still want to use a US IP or
if I want to be connected to one of my other servers without having the signal
bounce to the US and back.

After deleting my existing instance(which was at the european data center) I
looked at the available Community AMIs. One of them was called **OpenVPN
Access Server** and after looking at the related site I thought this is
exactly what I wanted and is free for 2 concurrent users. Theres also a
[guide](http://openvpn.net/index.php/access-server/docs/admin-guides/499
-openvpn-access-server-ami.html) on their site which describes how to make the
initial setup. And even better it perfectly fits in the Free Tier Plan.

Unfortunately I could nowhere find what the user is with which I can connect
via ssh to the instance. After some more searching and trying I figured its
the user **ubuntu** - nice of them to mention that nowhere in the guide.

But even without even having to connect a single time via SSH to the instance
it had started a nice webUI with full Admin interface and everything you need
to connect to the VPN. It even offers pre-configured OpenVPN Clients for
Windows and Mac and a guide for Unix.

So now all I have to do is tell the OpenVPN Client to connect to my instance
and I'm good to go. Now I just have to keep a look at my monthly traffic -
there are _only_ 15GB in and 15GB out in the Free Tier Plan. Could become a
problem considering the fact I now have access to hulu/pandora and others.

This usage doesn't has anything to do with my initial plan to explore the
cloud but an EC2 instance is basically just a virtual server with some
additional services strapped on. Still I will look into the other services of
the Free Tier Plan. I'm especially interested in the SimpleDB service,
unfortunately only 25 _machine hours_ are free per month - whatever they mean
with machine hour. There are more _more cloudy_ things I have in mind and will
test at some point.

PS: I also found a really nice monthly activities page for your account, shows
exactly what and how much of it you used and how much it costs.

