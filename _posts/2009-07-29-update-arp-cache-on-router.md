---
title: Update ARP cache on router
author: nedwards
layout: post
categories:
  - Linux
tags:
  - Linux
  - routing
---
A couple of times in the past I have had issues when migrating from one server to another behind a router. By this I mean bringing the interface of one server down and then assigning the same ip address to another server. So by doing this you do not have to change a dns records.

However there is sometimes as issue which is that the arp cache on the router is not updated with the new mac address, so the router is still looking for the old mac address.

In order to force an update on the router, run the following:

`sudo arping -U -I eth1 xxx.xxx.xxx.xxx `

On Debian Lenny this is in iputils-arping.

`sudo aptitude install iputils-arping`
