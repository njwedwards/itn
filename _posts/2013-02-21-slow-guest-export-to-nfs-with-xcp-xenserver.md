---
title: Slow guest export to NFS with XCP (Xenserver)
author: nedwards
layout: post
categories:
  - backup
  - Linux
tags:
  - NFS
---
For a while I had been wondering why &#8216;xe vm-export&#8217; was taking so long to export a vm to an NFS share. It turns out that I needed to add the &#8216;async&#8217; option under /etc/exports (or via the GUI with Openfiler). It seems (I&#8217;m guessing) to have increased the speed by about 10x when exporting a vm. I had not thought that it would have increased the performance that much. Incidentally when just copying a standard file there was no noticeable slowdown with the &#8216;sync&#8217; option set.

Ref: [http://tldp.org/HOWTO/NFS-HOWTO/performance.html][1]

 [1]: http://tldp.org/HOWTO/NFS-HOWTO/performance.html "NFS Performance"
