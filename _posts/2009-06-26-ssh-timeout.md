---
title: SSH Timeout
author: nedwards
layout: post
categories:
  - Bash
  - SSH
tags:
  - Bash
  - Linux
  - SSH
  - VPN
---
As I use ssh all the time. An issue that I sometimes get is that the vpn disconnects, and the ssh session just freezes and never disconnects. To combat this and to get the ssh client to disconnect if it does not receive anything from the server after a period of time, then add the following to /etc/ssh/ssh_config:

<pre>ServerAliveInterval 30
</pre>

The above should mean that it will disconnect after 30 seconds, however it seems to be a bit longer than that. Anyway it works.
