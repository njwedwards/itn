---
tags: [Notebooks/itblog]
title: Shorewall multiple zones for interface
created: '2019-09-29T11:18:03.629Z'
modified: '2019-10-18T14:22:56.699Z'
---

It is possible to have multiple zones for a specific interface with shorewall. This is helpful if you want run services on a local ip address behind a nat firewall. I think that you need at least shorewall 3 to do this.

/etc/shorewall/zones  
`<br />
fw	firewall<br />
net	ipv4<br />
loc:net ipv4<br />
`

/etc/shorewall/hosts  
`<br />
loc                 eth0:192.168.40.0/24<br />
`

This means that you can now distinguish between the local request (loc zone) and others (net zone).

In my case I am running a pptp server so I also have:

/etc/shorewall/hosts  
`<br />
net     eth0            detect          routefilter<br />
loc     ppp+<br />
`

The ppp+ means that this will apply to all ppp interfaces for connected users. They are treated a local users by shorewall.

/etc/shorewall/rules  
`<br />
...<br />
ACCEPT		net		$FW		tcp	1723<br />
ACCEPT		net		$FW		47<br />
...<br />
`

/etc/shorewall/policy  
`<br />
$FW		all		ACCEPT<br />
loc		$FW		ACCEPT<br />
loc		all		ACCEPT<br />
net		all		REJECT		info<br />
# The FOLLOWING POLICY MUST BE LAST<br />
all		all		REJECT		info<br />
`

References:

<http://www.shorewall.net/Multiple_Zones.html>  
<http://www.shorewall.net/PPTP.htm>
