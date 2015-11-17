---
title: Net-SNMP on OmniOS
author: nedwards
layout: post
categories:
  - Solaris
tags:
  - omnios
  - snmp
  - solaris
---
Install from repository:

> pkg install system/management/snmp/net-snmp

Add the following to /etc/net-snmp/snmp/snmpd.conf

> syscontact &#8220;user@domain&#8221;  
> syslocation &#8220;Location&#8221;
> 
> rocommunity public  
> rwcommunity private 127.0.0.1 

Enable the service

> svcadm enable net-snmp

Check that the service is running:

> netstat -an -P udp | grep 161

From another host do an snmp query:

> snmpwalk -v 2c -c public 192.168.1.5
