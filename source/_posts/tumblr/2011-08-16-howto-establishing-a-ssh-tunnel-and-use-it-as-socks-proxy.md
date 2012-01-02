--- 
layout: post
title: "HOWTO: establishing a SSH tunnel and use it as SOCKS proxy"
categories: 
- tumblr
- SOCKS
- proxy
- putty
- ssh
- tunnel
date: 2011-08-16
---
I have one last post regarding my plan to reroute certain web traffic through
my server.

This post maybe should have been the first in this little series, because I
will show you how to setup a SOCKS proxy to your server.

<!-- more -->

## Putty

I'd like to think that you already have a session which connects to your
server via ssh. Load this session and go in the menu to the item
**Connection** -> **SSH** -> **Tunnels**.

Enter the portnumber of your choice into the field **Source Port** for example
1234.

Than select _Dynamic_ and _Auto_ and click **Add**. You will now see **D1234**
in the list above.

You can now go back the the sessions screen, save your changes and open the
connection.

## unix

for unix it is quite simple

    
    ssh -ND 1234 user@server.com
    

This will open a SOCKS proxy on port 1234 to the server. **-N** Tells prevents
the console from executing any remote command. This way it will just open the
tunnel and than sits there and waits for you to close it (with CTRL+C) later.
With an additional **-f** it is also possible to completely background the
process, but than its not as easy for you to close the tunnel later.
