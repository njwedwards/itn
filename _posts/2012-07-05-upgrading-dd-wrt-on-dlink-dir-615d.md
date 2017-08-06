---
title: Upgrading DD-WRT on Dlink DIR-615d
author: nedwards
layout: post
geo_public:
  - 0
categories:
  - Firewall
  - Linux
  - PPTP
  - SSH
  - VPN
tags:
  - dd wrt
  - pptp server
  - ssh server
  - v24
---
I have been running quite an old build (&#8220;Firmware: DD-WRT v24-sp2 (11/21/10) std&#8221;) of DD-WRT for quite a while. I have wondered why there have been no updates to speak of. It has been working well generally.

However it turns out the builds are at ftp://dd-wrt.com/others/eko/BrainSlayer-V24-preSP2/

Yesterday I went in and downloaded and upgraded to the following:

ftp://dd-wrt.com/others/eko/BrainSlayer-V24-preSP2/2012/06-08-12-r19342/dlink-dir615d/dir615d-ddwrt-webflash.bin

It seemed to work, however the PPTP server did not work and also my Vonage phone was not working properly.

The releases since r18687 are using a 3.2.x kernel.

So today I went and tried the following build:

ftp://dd-wrt.com/others/eko/BrainSlayer-V24-preSP2/2011/12-14-11-r18007/dlink-dir615d/dir615d-ddwrt-webflash.bin

This solves the PPTP issue, however the SSH server does not work properly (REF: http://svn.dd-wrt.com/ticket/2279, http://svn.dd-wrt.com:8000/ticket/2283). I had a try but can&#8217;t get it to work, without starting it manually.

**UPDATE**  
The ssh server (dropbear) is actually working now after doing the following:

Turn off ssh  
rm /tmp/root/.ssh/ -fr  
nvram set sshd\_rsa\_host_key  
nvram set sshd\_dsa\_host_key  
commit  
Reboot  
Switch on ssh  
Reboot

**UPDATE 2014/08/27**

Issue caused by not having anything for &#8220;remoteip&#8221; in /tmp/pptpd/pptpd.conf

To run pptpd from cli:  
pptpd -c /tmp/pptpd/pptpd.conf -o /tmp/pptpd/options.pptpd


**UPDATE 2017/08/06**

The updated firmware is now at <ftp://ftp.dd-wrt.com/betas/2017/08-03-2017-r33006/dlink-dir615d/>