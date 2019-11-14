---
tags: [Notebooks/itblog]
title: Setting up Openfiler with 3x Dell MD1200 enclosures
created: '2019-09-29T11:18:04.465Z'
modified: '2019-10-18T14:22:56.627Z'
---

At work I have recently setup 3 Dell MD1200 storage enclosures. Each of these enclosures contains 12 3TB SAS drives. The external enclosures are connected via a Dell H800 card, the server being used is a Dell Poweredge 1950. The aim is to use the server primarily as a SAN, serving various ESXi hosts making use of iSCSI and NFS.

## Storage

I have decided to use Openfiler 2.99 on the server. It appears that the MegaRAID driver in the kernel is 00.00.04.28-RH1 which seems fairly up to date. 

You can check the module loaded using:

\# modinfo megaraid_sas

According to the Dell manual the Dell PERC H800 uses the LSI 2108 chipset. 

For the card info &#8216;lspci -nn&#8217; gives:

> 0e:00.0 RAID bus controller \[0104]: LSI Logic / Symbios Logic LSI MegaSAS 9260 [1000:0079\] (rev 05)

I have downloaded MegaCLI 8.02.21 from [here][1]. It is a zip containing binaries for many different platforms. After downloading you can do the following or similar:con

\# unzip 8.02.21_MegaCLI.zip  
\# cd 8.02.21\_Linux\_MegaCLI  
\# unzip MegaCliLin.zip

Install rpm if you have not already  
\# conary update rpm 

Try to install the following:  
\# rpm -ivh Lib_Utils-1.00-09.noarch.rpm  
\# rpm -ivh MegaCli-8.02.21-1.noarch.rpm

There will probably be unmet dependencies, so try to install those first. Once you have installed all you can you can force the install. In my case the only thing left was that it was looking for /bin/sh.

\# rpm -ivh Lib_Utils-1.00-09.noarch.rpm &#8211;nodeps  
\# rpm -ivh MegaCli-8.02.21-1.noarch.rpm &#8211;nodeps

MegaCLI should now be at the following path /opt/MegaRAID/MegaCli/MegaCli64. Test by running:

\# /opt/MegaRAID/MegaCli/MegaCli64 -AdpAllInfo -aALL 

Show info for all disks on controller 1 (my box has 2)  
\# /opt/MegaRAID/MegaCli/MegaCli64 -LdPdInfo -a1

Show info for specific disk (this example, Enclosure 41, Slot 7)  
\# /opt/MegaRAID/MegaCli/MegaCli64 -PdInfo -PhysDrv [41:7] -a1  
Rebuild progress  
\# /opt/MegaRAID/MegaCli/MegaCli64 -pdrbld -showprog -physdrv[41:7] -a1  
or for interactive  
\# /opt/MegaRAID/MegaCli/MegaCli64 -pdrbld -progdsply -physdrv[41:7] -a1

[Monitor Megaraid controller][2]  
[MegaRAID Help][3]

It has been my intention to provide a balance between storage space, flexibility and redundancy for this storage array. As this was the case I decided to configure the setup as two raid volumes, one 24 disk with raid 6 and one 12 disk with raid 5.

### Monitoring

The following has been added to /etc/crontab, so that every hour the system will check if there are any failed or degraded files and will send an email if there are.

`0 * * * *	root	/opt/MegaRAID/MegaCli/MegaCli64 -AdpAllInfo -aALL | egrep "(Degraded|Failed).*:.*[1-9]" && echo "RAID issue on $(hostname)" | mail root -s "RAID issue on $(hostname)"`

#### Notification setup

Notification has been setup under System &#8211; Notification. Also I have set the email address of the person to get mail sent to root, this is set in /etc/aliases:

`<br />
....<br />
# Person who should get root's mail<br />
root:		user@domain.com<br />
....<br />
`

Another thing which needed to be set was to add a fully qualified domain to /etc/hosts. If this is not set to a real domain then it could cause an issue with some mail servers receiving mail.

### Initial testing

As an initial test, I took out various drives from the first raid device (raid 6). As expected when I took out the 3rd drive, the raid device disappeared. I then rebooted the server and had to go into the H800 card setup utility to import the foreign configuration back in. The volume configuration that it had was in red and 3 drives were marked as missing. Once I had imported the foreign configuration back in, the drives started to rebuild and I could see the device (and files) again when the server had booted back into Openfiler

#### Speed

Using hdparm I can get the read speed of the drives:

> [root@das share]# hdparm -t /dev/sdb
> 
> /dev/sdb:  
> Timing buffered disk reads: 1768 MB in 3.00 seconds = 588.93 MB/sec  
> [root@das share]# hdparm -t /dev/sdc
> 
> /dev/sdc:  
> Timing buffered disk reads: 1782 MB in 3.00 seconds = 593.39 MB/sec

Using dd on xfs filesystem:

Write speed

> [root@das share]# dd if=/dev/zero of=outfile5 count=256 bs=8192k  
> 256+0 records in  
> 256+0 records out  
> 2147483648 bytes (2.1 GB) copied, 5.42203 s, 396 MB/s 

Read speed

> [root@das share]# dd of=/dev/zero if=outfile5 bs=8192k  
> 256+0 records in  
> 256+0 records out  
> 2147483648 bytes (2.1 GB) copied, 3.5116 s, 612 MB/s 

After a snapshot is made of the filesystem the speed is reduced significantly:

> [root@das share]# dd if=/dev/zero of=outfile6 count=256 bs=8192k  
> 256+0 records in  
> 256+0 records out  
> 2147483648 bytes (2.1 GB) copied, 16.8945 s, 127 MB/s  
> [root@das share]# dd of=/dev/zero if=outfile6 bs=8192k  
> 256+0 records in  
> 256+0 records out  
> 2147483648 bytes (2.1 GB) copied, 5.6502 s, 380 MB/s 

Ref: [http://www.nikhef.nl/~dennisvd/lvmcrap.html][4]  
[][5]

## Network

The storage network has been setup using 2 1Gb ethernet connections to two separate Dell Powerconnect M6348 switches. They have been configured as a bonded device on Openfiler using 802.3ad (LACP). This means that the traffic should be shared over both links and add redundancy.

Network refs:  
[http://support.dell.com/support/edocs/network/m8024k/en/ucg/html/linkagg.htm][6]  
[http://backdrift.org/howtonetworkbonding][7]

### Initial testing

It seems that frames are shared over both physical interfaces when traffic goes over the bonded interface (bond0). There is also no loss of connectivity when one of the physical connections are disconnected.

Further investigation will need to be done to ascertain the maximum speed of the bonded link.

Helpful links:

[PowerVault™ MD1200 Guides][8]  
[Poweredge H800 Guides][9]  
[Readme for Dell H700/H800 Device Driver for Linux (00.00.04.31.2-1)][10]  
[H800 Linux Driver][11]

 [1]: http://www.lsi.com/support/products/Pages/MegaRAIDSAS9260-8i.aspx
 [2]: http://blog.mechanised.com/2010/04/how-to-monitor-lsi-megaraid-controller.html "Monitoring post"
 [3]: http://thatlinuxbox.com/blog/article.php/lsi-megaraid-megacli
 [4]: http://www.nikhef.nl/~dennisvd/lvmcrap.html "http://www.nikhef.nl/~dennisvd/lvmcrap.html"
 [5]: http://johnleach.co.uk/words/613/lvm-snapshot-performance "http://johnleach.co.uk/words/613/lvm-snapshot-performance"
 [6]: http://support.dell.com/support/edocs/network/m8024k/en/ucg/html/linkagg.htm "Configuring Link Aggregation"
 [7]: http://backdrift.org/howtonetworkbonding "How to configure network bonding in Linux"
 [8]: http://support.dell.com/support/edocs/systems/md1200/en/index.htm
 [9]: http://support.dell.com/support/edocs/storage/Storlink/H700H800/en/index.htm
 [10]: http://ftp.dell.com/sas-raid/R282636-megaraid_sas-00.00.04.31.2-1.txt "Dell H700/H800 Device Driver for Linux (00.00.04.31.2-1)"
 [11]: http://ftp.dell.com/sas-raid/R282636-megaraid_sas-00.00.04.31.2-1.tar.gz
