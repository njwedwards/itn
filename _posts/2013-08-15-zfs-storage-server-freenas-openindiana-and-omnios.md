---
tags: [Notebooks/itblog, solaris]
title: 'ZFS storage server &#8211; FreeNAS, Openindiana and OmniOS'
created: '2019-09-29T11:18:05.400Z'
modified: '2019-10-18T14:33:28.021Z'
---

Having played about with ZFS on Linux previously and wanting to try out a new backup storage solution, I decided to install a new server. One that would be a good fit for ZFS and also preferably give some sort of front-end to help with configuration.  Having looked around at options it appeared that FreeNAS or a Solaris derivative (Openindiana or OmniOS) were the ways to go.

After some reading I decided on FreeNAS (9.1 RC2 x64). I downloaded and eventually installed onto a usb drive.

All seemed to work fairly well, and I created a striped pool with 2x 1TB SATA disks. 

However after a period of time NFS read and writes to the pool were very erratic and quite slow. It was not consistent and on a large copy the IO on the disk would go up and down a lot. I tried turning off sync and that did help, but did not solve the problem. I also tried some other options (no compression, dedup off etc), but nothing really helped. I did some searching but in the end I wanted something that just worked.

Next I tried Openindiana. After installing and configuring it enough to test, the performance was really good. I quite liked it however from my reading it appeared that development had somewhat stalled. So after more searching I came across OmniOS, which is under ongoing development.

The install and feel of OmniOS was pretty much the same as Openindiana however it just seemed a bit more polished. Performance was good and I went ahead also and installed the Napp-it frontend.

I have not really used a Solaris type operating system by choice before, but I have to say I am quite enjoying it. I have only been using for just over a week so time will tell how well it performs as the ZFS solution I had envisaged.

 

 
