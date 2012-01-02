--- 
layout: post
title: "HOWTO: configuring a local SOCKS Proxy in your browser"
categories: 
- tumblr
- IE9
- browser
- firefox
- opera
- proxy
- socks
- safari
date: 2011-08-14
---
as a follow up on my last post I thought I describe how to setup a local proxy
for a ssh tunnel in the most common browsers

To use the tunnel you will have to configure the browsers to use a SOCKS
proxy. For this post I will have my local proxy at 127.0.0.1:1234 (or
localhost:1234)

<!-- more -->

## Opera

  1. **Settings** -> **Preferences** (or simply CTRL+F12)
  2. **Advanced** -> **Network** -> **Proxy Servers
  3. check **SOCKS**
  4. fill in "127.0.0.1" and "1234" in the field next to SOCKS, keep the other fields empty

Opera doesn't use the proxy settings for local addresses on default.

## Firefox

  1. **Options** -> **Advanced** -> **Network** -> **Settings…**
  2. choose **Manual proxy configuration**
  3. enter "127.0.0.1" into SOCKS Host
  4. enter "1234" into the Port field next to the SOCKS host
  5. choose **SOCKS v5**
  6. enter "localhost, *.local" into the field next to "No Proxy for:"

## Chrome, Safari and IE9 (windows)

  1. tool-icon -> **Options** -> **Under the Hood** -> **Change proxy settings…**(Chrome)  
gear-icon -> **Preferences** -> **Advanced** -> Proxies: **Change Settings…**
(Safari)

gear-icon -> **Internet Options** -> **Connections** (IE9)

  2. **LAN Settings**
  3. check **Use a proxy for your LAN(…)**
  4. click **Advanced**
  5. uncheck **Use the same proxy server for all protocols**
  6. check **bypass proxy server for local addresses**
  7. fill in "127.0.0.1" and "1234" in the field next to Socks, keep the other fields empty

These three browsers basically use the system proxy configuration. So with
this setup all other software which also uses these settings will also use the
proxy.

_All the above is done with the latest versions of the browsers at the moment
so consider this if you use another version.(Opera 12.00 pre-alpha 1024 |
Chrome 15.0.849.0 canary | Firefox Aurora 7.0a2 (2011-08-14) | Safari 5.1
7534.50)_

