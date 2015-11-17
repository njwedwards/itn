---
title: ARP issue with xen bridge
author: nedwards
layout: post
categories:
  - Uncategorized
---
I have been using Xen with network bridging for a while and things have been working well. However I started to see strange behaviour on a specific new guest (domU). Connectivity on the public bridged interface would be intermittent. Up for a while and then down for a while. It turns out that some arp queries were not being answered and so the guest (domU) host did not know the mac address for a particular ip (the gateway) for a period of time. I then observed this on other hosts.

After much digging and looking at tcpdump output, I set the arp address manually on the affected guests. After a while though I decided to specify the network bridges in Debian, instead of letting the Xen scripts do their work as I had heard that they can cause issues.

So to add two bridge interfaces, one with an ip and one without, add the following to /etc/network/interfaces

`<br />
auto br-eth0<br />
iface br-eth0 inet static<br />
address 192.168.xxx.xxx<br />
netmask 255.255.255.0<br />
gateway 192.168.xxx.xxx<br />
bridge_ports eth0</p>
<p>auto br-eth1<br />
iface br-eth1 inet manual<br />
  bridge_ports eth1</p>
<p>`

Now that I have done this the problem has not reappeared as yet. I still don&#8217;t know exactly why this was happening.
