---
tags: [Notebooks/itblog]
title: Securely wiping disks
created: '2019-09-29T11:18:04.879Z'
modified: '2019-10-18T14:22:56.555Z'
---

I needed to wipe all the data from a set of Dell servers.

I decided to use [DBAN][1]. It gives you quite a lot of different methods to securely wipe your hard disks.

For a RAID controller is it recommended that you ensure that the disks are in [JBOD (or Single)][2] mode. For the Dell h700 this can be done under setup by creating a volume for each disk and setting to RAID 0.

When first attempting I was getting &#8216;process crash&#8217; error messages. I attempted to fix by removing the unknown devices that were showing by setting iDRAC media to [disabled][3] in the iDRAC settings. However even after changing this, DBAN was still not playing ball.

I then found [Nwipe][4] which is a fork of DBAN. It comes as part of Parted Magic.

For some reason Parted Magic would not boot with normal mode so I had to use the &#8216;Failsafe 64&#8242; boot option. Once it was booted I could get to the Nwipe screen by typing &#8216;nwipe&#8217; at the command line. Once in, the interface is the same a DBAN. I selected all 12 disks to wipe and used the default method dod (3 pass plus a blanking pass). After it had settled it estimated that it was going to take another 45 hours!

UPDATE: It took around 59 hours, to wipe 12 1TB SATA disks.

 [1]: http://www.dban.org/
 [2]: http://en.wikipedia.org/wiki/Non-RAID_drive_architectures
 [3]: http://bmaupin.wordpress.com/2010/11/22/dban-error-devsda-process-crash/
 [4]: http://www.andybev.com/index.php/Nwipe
