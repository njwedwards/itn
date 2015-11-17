---
title: Using tar and output
author: nedwards
layout: post
categories:
  - backup
---
By default tar will complain about the leading / in filenames (/bin/tar: Removing leading \`/&#8217; from member names). To ensure this does not happen use:

/bin/tar -jcf file.tar.bz2 -C / etc/ 

instead of:

/bin/tar -jcf file.tar.bz2 /etc 

[http://www.linuxtopia.org/online\_books/linux\_tool\_guides/tar\_user_guide/absolute.html][1]

 [1]: http://www.linuxtopia.org/online_books/linux_tool_guides/tar_user_guide/absolute.html
