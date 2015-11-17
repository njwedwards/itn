---
title: Ubuntu 8.04 install issue
author: nedwards
layout: post
categories:
  - Linux
tags:
  - Linux
  - ubuntu
---
I was trying to install Ubuntu 8.04 again today on a Dell Optiplex n755 machine. This machine also has a floppy drive.

I had a error with the install trying to mount /dev/fd0, failing and thus loading busybox.

In order to fix this add &#8220;break=mount&#8221; to the boot arguments and then when the startup seems to stall type:

> rmmod floppy  
> exit 

After this the install should carry on and you can install. A relief as I had tried all sort to get this to work.
