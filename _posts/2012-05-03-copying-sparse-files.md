---
tags: [Notebooks/itblog]
title: Copying sparse files
created: '2019-09-29T11:18:04.467Z'
modified: '2019-10-18T14:22:56.123Z'
---

As I have been dealing a lot with VMware recently, I have come across issues when copying the [sparse][1] files that are created when you create a thin provisioned disk in VMware ESXi.

The problem has been that when you do a copy (cp) in Linux, the command tries to read all of the data from the file, even when there is nothing in most of it, which is the case in a fairly empty sparse file. This would not normally be an issue but becomes one when you have multiple 2TB files!

After a lot of trawling through the internet, it appears that there is a solution in later versions on [Coreutils][2]. I have downloaded a recompiled 8.13 and just used the new cp command.

Using the new cp it is possible to copy a sparse (10G) file in a fraction of the time.

With old cp version 5.2.1 (Openfiler 2.3)

> [root@openfiler test]# time cp test-flat.vmdk ../copy
> 
> real 0m13.558s  
> user 0m1.560s  
> sys 0m11.829s

With new cp version 8.13

> [root@openfiler test]# time cp-new test-flat.vmdk ../copy
> 
> real 0m0.153s  
> user 0m0.000s  
> sys 0m0.000s

By using strace you can see that the difference is in the amount of times the OS has to try to read the file:

> [root@openfiler test]# strace -e lseek cp test_1-flat.vmdk ../non 2>&1 | wc -l  
> 2621440

That means it does the following 2621440 times!

> lseek(4, 4096, SEEK_CUR) = 752476160

With the new version it only reads what it needs to.

I think it&#8217;s all to do with cp making use of FIBMAP ioctl. With a fairly recent version of hdparm you can use:

> <pre>[root@das share1]# sudo hdparm --fibmap Disk-flat.vmdk</p>


<p>
  Disk-flat.vmdk:<br />
   filesystem blocksize 4096, begins at LBA 0; assuming 512 byte sectors.<br />
   byte_offset  begin_LBA    end_LBA    sectors<br />
             0 3584444328 3584444583        256<br />
        131072 3584445352 3584455143       9792<br />
       5144576 3584444584 3584444903        320<br />
       5308416 3584455144 3584461159       6016<br />
  1099516706816 3584444904 3584444967         64<br />
  1099516870656 3584445224 3584445351        128
  
  
  <pre></blockquote>


<p>
  Refs:<br />
  http://lists.gnu.org/archive/html/coreutils/2011-02/msg00056.html<br />
  http://serverfault.com/questions/29886/how-do-i-list-a-files-data-blocks-on-linux
</p>

 [1]: https://wiki.archlinux.org/index.php/Sparse_file
 [2]: http://www.gnu.org/software/coreutils/
