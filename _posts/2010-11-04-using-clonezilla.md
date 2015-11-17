---
title: Using Clonezilla
author: nedwards
layout: post
categories:
  - Uncategorized
---
I have just had the task of configuring 50 netbooks for a specific purpose. As I had already done a few of these before I knew it would be a good idea to try to clone one of the disks and use this on the others.

I came across Clonezilla a while back, and basically it&#8217;s an open source alternative to Norton Ghost. You can run it as a server or on a cd or usb drive. I decided to use the server option as I had so many netbooks to setup.

The first thing I did was install on a Ubuntu 10.04 virtual machine using some helpful instructions from [here][1].

After cloning a configured install, I connected the server to a separate 8 port gigabit switch. From what I could see it needs it&#8217;s own switch as the server needs to run dhcp. I was able to restore the image to multiple devices at once using the multicast option, meaning that the data stream is sent to all the devices at once.

All in all, I&#8217;m really impressed with Clonezilla and will definitely use it again if doing something similar.

*NOTE: When doing the multicast restore the speed was around 14.5MB/s, a bit slower than I would have thought for a gigabit switch, but still plenty fast enough and there may have been some way to increase this.*

 [1]: http://www.howtoforge.com/cloning-linux-systems-with-clonezilla-server-edition-clonezilla-se
