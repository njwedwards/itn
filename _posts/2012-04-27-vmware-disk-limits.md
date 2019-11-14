---
tags: [Notebooks/itblog]
title: VMware disk limits
created: '2019-09-29T11:18:04.466Z'
modified: '2019-10-18T14:22:57.218Z'
---

It appears that the vmdk limit on ESXi 4.1 (and 5) is around 2TB (2TB &#8211; 512Bytes).

It makes no difference if it is being stored on NFS with a file system that supports a larger file either.  
<http://communities.vmware.com/thread/325941>

In order to create the largest possible disk, just creating a 2TB disk does not work. In ESXi 4.1 the largest I could create was by using 2097151MB, which is 2TB &#8211; 1MB.

Other refs:  
<http://blog.axiomdynamics.com/2011/09/vmware-vsphere-and-esx-vmdk-size-limit.html>  
<http://communities.vmware.com/thread/165526>  
[http://www.vmware.com/pdf/vsphere4/r41/vsp\_41\_config_max.pdf][1]  
<http://www.vmware.com/pdf/vsphere5/r50/vsphere-50-configuration-maximums.pdf>

 [1]: http://www.vmware.com/pdf/vsphere4/r41/vsp_41_config_max.pdf
