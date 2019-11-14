---
tags: [Notebooks/itblog]
title: Using tar and output
created: '2019-09-29T11:18:02.578Z'
modified: '2019-10-18T14:22:57.185Z'
---

By default tar will complain about the leading / in filenames (/bin/tar: Removing leading \`/&#8217; from member names). To ensure this does not happen use:

/bin/tar -jcf file.tar.bz2 -C / etc/ 

instead of:

/bin/tar -jcf file.tar.bz2 /etc 

[http://www.linuxtopia.org/online\_books/linux\_tool\_guides/tar\_user_guide/absolute.html][1]

 [1]: http://www.linuxtopia.org/online_books/linux_tool_guides/tar_user_guide/absolute.html
