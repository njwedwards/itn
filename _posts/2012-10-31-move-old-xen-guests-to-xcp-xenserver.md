---
tags: [linux, Notebooks/itblog]
title: Move old Xen guests to XCP (Xenserver)
created: '2019-09-29T11:18:04.775Z'
modified: '2019-10-18T14:32:13.471Z'
---

I have been looking at moving some old paravirtualised Xen guests (running Debian Lenny) from a host running Xen 3.2.1 and Xen Tools 3.9 to a new host runnning XCP 1.6.

It has not proved to be as simple as expected. However it should be possible following the (rough) notes below.

If possible first ensure that grub and the xen-kernel are installed on the existing guest. Important in my case as my guests were using the kernel from dom0.

On the existing host download xva.py available from http://www.xen.org/files/xva/ .

After reading the README you can run as follows:

\# python xva.py &#8211;sparse -c /etc/xen/guest.cfg -f /transfer/guest.xva

Then transfer the created guest.xva to the new host and on the new host run:

\# xe vm-import filename=guest.xva sr-uuid=

(the sr-uuid can be gathered from running xe sr-list)

When the guest has been imported it should be available under XenCenter. From my experience it seems that it is not possible to use a boot iso with a paravirtualised guest and so what I did is create a new temporary guest without a disk and then just booted with an iso image (Finnix in my case).

Detach the root disk (where the kernel is) from the imported guest, attach it to the temporary guest (with iso) and boot.

Now in the temp guest do the following (or similar):

\# mount /dev/sda /mnt  
\# mount -t proc proc /mnt/proc/  
\# mount -t sysfs sys /mnt/sys/  
\# mount -o bind /dev /mnt/dev/  
\# chroot /mnt  
\# update-grub # to create /boot/grub/menu.lst

*NOTE: On one guest when I ran update-grub it complained that /dev/xvda did not exist. I don&#8217;t know why as there was no reference to it. In this case I have to add /boot/grub/menu.lst manually by copying it from another server.*

Now update the disk references in /etc/fstab and /boot/grub/menu.lst .

Once done shutdown and attach disk back to the imported guest at device 0.

*NOTE: For Pygrub to work correctly the root filesystem containing the /boot/grub files must be on the first disk/partition.*

Also ensure that the Xen guest OS boot parameters are correct, mine is:

root=/dev/xvda ro clocksource=jiffies
