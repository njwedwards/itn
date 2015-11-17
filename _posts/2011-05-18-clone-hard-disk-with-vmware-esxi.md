---
title: Clone hard disk with VMware ESXi
author: nedwards
layout: post
categories:
  - Uncategorized
---
I have been using VMware ESXi (4.1) a lot recently and have been using disk clones so that I don&#8217;t have to do a new OS install every time.

The issue is that I am using thin provisioning and when you do a copy if you are using NFS then it will change and allocate all of the space in the resulting copy. Not helpful!

So to get around this you can use vmkfstools. You will need to perform the following on a hard disk that is part of an existing machine otherwise you will get the following error:

`DiskLib_Check() failed for source disk The system cannot find the file specified (25).<br />
that the machine `

Use the following to do a thin provisioned clone of a disk.  
`<br />
vmkfstools -i original.vmdk -d thin ../newmachine/copy.vmdk<br />
`

What I tend to do is to do a snapshot after I have created the virtual machine (original). I can then do a clone on a running machine as everything after the snapshot will be written to a delta file that just contains the changes after the snapshot.
