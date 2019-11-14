---
tags: [Notebooks/itblog]
title: Issue with new Nvidia G210 card installed on media pc
created: '2019-09-29T11:18:04.637Z'
modified: '2019-10-18T14:22:56.323Z'
---

After installing a new Nvidia G210 card in my media pc, the machine was not working right. The keyboard and mouse were very slow and the usb wifi was not working.

I eventually found that it was caused by:

> Jun 16 11:48:39 media kernel: [ 13.615995] irq 19: nobody cared (try booting with the &#8220;irqpoll&#8221; option)  
> Jun 16 11:48:39 media kernel: [ 13.616002] Pid: 870, comm: apparmor_parser Not tainted 3.2.0-23-generic #36-Ubuntu  
> Jun 16 11:48:39 media kernel: [ 13.616005] Call Trace:  
> Jun 16 11:48:39 media kernel: [ 13.616007] <IRQ> [<ffffffff810db37d>] _\_report\_bad_irq+0x3d/0xe0  
> Jun 16 11:48:39 media kernel: \[ 13.616017\] \[<ffffffff810df9df>\] ? rcu\_check\_quiescent_state+0x2f/0xd0  
> Jun 16 11:48:39 media kernel: \[ 13.616017\] \[<ffffffff810db605>\] note_interrupt+0x135/0x190  
> Jun 16 11:48:39 media kernel: \[ 13.616017\] \[<ffffffff810d8e69>\] handle\_irq\_event_percpu+0xa9/0x220  
> Jun 16 11:48:39 media kernel: \[ 13.616017\] \[<ffffffff8106e97d>\] ? _\_do\_softirq+0xfd/0x210  
> Jun 16 11:48:39 media kernel: \[ 13.616017\] \[<ffffffff810d9031>\] handle\_irq\_event+0x51/0x80

After adding irqpoll to the boot options in my /boot/grub/grub.cfg all was fine.
