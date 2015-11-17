---
title: ssh login delay
author: nedwards
layout: post
categories:
  - Linux
---
Sometimes I get a delay when trying to login to a Linux server using SSH.

A good way around this is to use the following in /etc/ssh/sshd_config:

`UseDNS no<br />
`

The issue here is that the server tries to do a reverse dns lookup on your ip address and in some cases it does not get a reply so this takes time. You can check that this is the case by running:

`host 192.168.40.1<br />
`

In my case it look 20 seconds and I received a:  
`192.168.40.1 does not exist (Authoritative answer)`

This is because the /etc/hosts file on the server contains:

`hosts:          files dns`

Which means that the /etc/hosts file is first checked, followed by the dns servers listed in /etc/nsswitch.conf. When the dns servers were queried they did not return a response or the system was waiting for too long for a host that does not exist on the public internet.
