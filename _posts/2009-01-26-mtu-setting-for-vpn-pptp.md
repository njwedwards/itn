---
tags: [Notebooks/itblog]
title: MTU setting for VPN (pptp)
created: '2019-09-29T11:18:03.630Z'
modified: '2019-10-18T14:22:56.418Z'
---

I had an issue with stalling connections from Ubuntu Intrepid, connecting to a Poptop pptp server. The issue was arising when using ssh, doing an scp transfer or when browsing over http.

The mtu setting was set too high (1496), however was fixed with the following.

In /etc/ppp/options file change the line:

#mtu 

with

mtu 1416

Ref:

[http://en.wikipedia.org/wiki/Maximum\_transmission\_unit][1]  
<http://ubuntuforums.org/archive/index.php/t-967826.html>

 [1]: http://en.wikipedia.org/wiki/Maximum_transmission_unit
