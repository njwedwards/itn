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

The above command may not work that relaibly if you have low memory, the following can be used instead:

	dd if=/dev/zero of=/tmp/test bs=1M count=1000 oflag=direct

Another helpful command for write and then read speeds:

	dd if=/dev/zero of=/tmp/output bs=10k count=100k; echo 3 | tee /proc/sys/vm/drop_caches; dd if=/tmp/output of=/dev/null; rm -f /tmp/output;

Also ref [http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=1008885](http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=1008885)
