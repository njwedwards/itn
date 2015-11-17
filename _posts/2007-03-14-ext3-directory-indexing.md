---
title: Ext3 Directory Indexing
author: nedwards
layout: post
categories:
  - Uncategorized
---
At work we run Courier IMAP and for a long time things have run quite slowly when the directory has more than a couple of thousand messages in it. A while back I discovered the dir_index option for the ext3 file system. Well today I enabled this on the partition that serves the email and the performance is like lightning now compared to what it was. My inbox now takes about 0.7 seconds to load via the webmail compared to what it was before which was 3 or 4 seconds at least.

**Update, as I have been using this further I have noticed that the fast load times are not always the case especially on folders that change often like the inbox.**

To check if this is enabled run:  
tune2fs -l /dev/hdaX | grep features  
If dir_index appears then it enabled

To enable it run:  
umount /dev/hdaX  
tune2fs -O dir_index /dev/hdaX  
e2fsck -fD /dev/hdaX  
mount /dev/hdaX

When I did it I only ran tune2fs -O dir_index /dev/hdaX and this seemed to work fine. I think it just starts creating the indexes when you look in a directory.
