---
title: Setting up tftp server on Centos
author: nedwards
layout: post
categories:
  - backup
  - Linux
tags:
  - enterprise-it
  - trivial file transfer
  - trivial file transfer protocol
---
When setting up the default tftp server on Centos Linux I have had issues. 

The server will be used for backing up config files from Cisco and similar devices.

After installing check the following if you have issues.

`<br />
[root@backup config]# cat /etc/xinetd.d/tftp<br />
# default: off<br />
# description: The tftp server serves files using the trivial file transfer<br />
#       protocol.  The tftp protocol is often used to boot diskless<br />
#       workstations, download configuration files to network-aware printers,<br />
#       and to start the installation process for some operating systems.<br />
service tftp<br />
{<br />
        disable = no<br />
        socket_type             = dgram<br />
        protocol                = udp<br />
        wait                    = yes<br />
        user                    = root<br />
        server                  = /usr/sbin/in.tftpd<br />
        server_args             = -c -s /zpool/backup/config -v -v<br />
        per_source              = 11<br />
        cps                     = 100 2<br />
        flags                   = IPv4<br />
}<br />
`

The files will be stored in /zpool/backup/config and you will need to ensure that &#8216;-c&#8217; is used so that the server will allow new files to be created.

Also as I was using a different path than the default. So I needed to run:

`<br />
chmod 777 /zpool/backup/config<br />
chown nobody /zpool/backup/config<br />
`

This is important otherwise you may receive a:

> Jul 3 12:07:38 backup in.tftpd[14059]: sending NAK (0, Permission denied) to 192.168.250.2
