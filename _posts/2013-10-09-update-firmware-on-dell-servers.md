---
title: Update firmware on Dell servers
author: nedwards
layout: post
categories:
  - Dell
  - Hardware
  - Linux
  - Solaris
tags:
  - dell
  - hardware
  - Linux
  - update
---
We run Linux a lot on Dell servers but also now Omnios (Solaris). Had an issue on a server and wanted to update the firmware. There did not appear to be an easy way to do this when not running (Linux/Windows).

What I did find was that there is a Dell (unoffical) Centos LiveCD, containing the latest firmware (related to Poweredge servers I think), that can be booted and will give you the option to update the firmware easily.

Refer to following pages for more info:

http://en.community.dell.com/techcenter/b/techcenter/archive/2011/08/17/centos-based-livedvd-to-update-firmware-on-dell-servers.aspx  
http://en.community.dell.com/techcenter/b/techcenter/archive/2012/09/06/centos-based-firmware-livedvd-with-om-7-1.aspx

Or you can just download the latest iso [here][1]

The LiveCD does take quite a while to boot, but once it has it will display a windows showing you what firmware updates can be made.

Very helpful <img src="http://itn.uk.to/wp-includes/images/smilies/simple-smile.png" alt=":-)" class="wp-smiley" style="height: 1em; max-height: 1em;" />

UPDATE:

In order to update the BMC controller on an old PE SC1425 I had to use the Centos 5.6 i386 livecd and ensure that I installed &#8216;compat-libstdc++-33.i386&#8242;. Before doing this I had tried to install the .BIN file in other version of Centos and Ubuntu but could not get it to work.

 [1]: http://linux.dell.com/files/openmanage-contributions/om73-firmware-live/Centos64-OM73-Firmware-LiveDVD.x86_64-1.1.0-Build8.1.iso "http://linux.dell.com/files/openmanage-contributions/om73-firmware-live/Centos64-OM73-Firmware-LiveDVD.x86_64-1.1.0-Build8.1.iso"
