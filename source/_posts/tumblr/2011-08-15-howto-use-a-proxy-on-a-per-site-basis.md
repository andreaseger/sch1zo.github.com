--- 
layout: post
title: "HOWTO: use a proxy on a per-site basis"
categories: 
- tumblr
- proxy
- socks
- opera
- firefox
- chrome
- safari
- IE9
date: 2011-08-15
---
in my last post I described how to setup a SOCKS proxy which only gets used on
some specific sites.

For example you only want to use the proxy if you got to "hulu.com" and
"pandora.com".

<!-- more -->

_I assume you at the moment you have setup the proxy as described in my last
post_

The in my opinion most obvious solution is to use a [Proxy auto-
config](http://en.wikipedia.org/wiki/Proxy_auto-config)-file. Unfortunately
this will not work in all browsers.

First lets take a look at the **proxy.pac** file:

```
function FindProxyForURL(url, host)
{
  // Use Proxy?
  if (dnsDomainIs(host, ".hulu.com") || dnsDomainIs(host, ".pandora.com")){
    return "SOCKS 127.0.0.1:1234";
  } else {
    return "DIRECT";
  }
}
```

It returns the SOCKS address if its hulu or pandora otherwise it goes directly
to the site. Save that file somewhere local or on a webserver.

Setting up the Browsers:

## Firefox

  1. **Options** -> **Advanced** -> **Network** -> **Settings…**
  2. choose **"Automatic proxy configuration URL:"**
  3. enter a url or filepath to your proxy.pac

## Opera

Opera also is able to use pac files, but due to it lack of SOCKS proxy support
for a long time(Only got it with version 11) it does not support SOCKS proxies
within a pac file. But there is a nice workaround.

  1. **Settings** -> **Preferences** (or simply CTRL+F12)
  2. **Advanced** -> **Network** -> **Proxy Servers**
  3. check **SOCKS**
  4. fill in "127.0.0.1" and "1234" in the field next to SOCKS, keep the other fields empty (this is exactly how to set it up permanently)
  5. click **Exception List**
  6. choose **Only use proxy for servers on the list**
  7. finally add pandora.com and hulu.com to that list.

So instead of using the auto-config file you can use a whitelist. It can also
be used the other way around as blacklist.

## Chrome, Safari and IE9 (windows)

There is an option within the system LAN Settings to use a automatic
configuration script, but all three browsers completely ignore that script.
They should be able to configure a SOCKS Proxy via a pac file but it didn't
work for me. I also didn't find another way to do a per-site proxy
configuration.

_Update:_ I had a look at the proxy settings in Chrome with Ubuntu running
gnome-shell. There is also a option to use a pac file but again the above
settings will just be ignored.

_Update 2:_ it seems this does not work anymore with hulu

_All the above is done with the latest versions of the browsers at the moment
so consider this if you use another version.(Opera 12.00 pre-alpha 1024 |
Chrome 15.0.849.0 canary | Firefox Aurora 7.0a2 (2011-08-14) | Safari 5.1
7534.50)_

