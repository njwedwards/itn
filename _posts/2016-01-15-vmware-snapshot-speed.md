---
title: VMware snapshot speed
author: nedwards
layout: post
published: true
---


## VMware snapshot speed

A user notified me that write speed was slow on a VMware ESXi 5.5 guest.

It appears that snapshots were the culpret. Using local storage with a snapshot the write speed (using dd) was 15MB/s and without it was running at 60MB/s.

dd command for reference:
	
	dd if=/dev/zero of=/tmp/test bs=1G count=1 oflag=direct

Also ref [http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=1008885](http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=1008885)
