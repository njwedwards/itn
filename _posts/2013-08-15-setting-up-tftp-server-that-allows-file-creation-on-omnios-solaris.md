---
tags: [Notebooks/itblog, solaris]
title: Setting up tftp server that allows file creation on OmniOS (Solaris)
created: '2019-09-29T11:18:05.399Z'
modified: '2019-10-18T14:33:22.862Z'
---

Following on from my previous post on installing [TFTP on Centos][1].

I went ahead and installed the default version, however it does not allow clients to add new files. I had to therefore to compile tftpd-hpa as I could not find an appropriate pre-complied package. The following steps should work:

Install development packages on OS:

> pkg install  
> developer/gcc47  
> developer/object-file  
> developer/linker  
> developer/library/lint  
> developer/build/gnu-make  
> system/header  
> system/library/math/header-math

Ref: http://omnios.omniti.com/wiki.php/DevEnv

Download the latest version from <https://www.kernel.org/pub/software/network/tftp/tftp-hpa/>

Install:

> tar -zxvf tftp-hpa-5.2.tar.xz  
> cd tftp-hpa-5.2  
> ./configure  
> make  
> make install

*After install, and after a lot of trial and error the following seemed to work to get it up and running:*

> in.tftpd -p -l -c -s /export/backup/config 

*Then I just needed to get it to work with the svcs scripts.*

Edit /etc/inet/inetd.conf and add the following line:

> tftp dgram udp6 wait root /usr/sbin/in.tftpd in.tftpd -p -c -s /export/backup/config

Run inetconv to create smf service manifest

> inetconv

Import created service manifest

> svccfg import /lib/svc/manifest/network/tftp-udp6.xml

Enable service

> svcadm enable svc:/network/tftp/udp6:default

*After the steps it maybe an idea to reboot as I could not get the smf to update correctly, although I am not that familiar with it.*

If you need to delete the service profile it can be done as follows:

> svccfg delete svc:/network/tftp/udp6:default

 [1]: /2012/07/03/setting-up-tftp-server-on-centos/
