---
tags: [Notebooks/itblog]
title: Bash scripting commands
created: '2019-09-29T11:18:02.579Z'
modified: '2019-10-18T14:22:56.013Z'
---

Working on commands today, I have found that the use of backticks (\`) in bash has been superseded by the following:

The use of $( command )

The following use will interpolate $NETWORK:  
CONNIP=$(/bin/ip addr | grep &#8220;inet 192.168.$NETWORK&#8221; | awk &#8216;{print $2;}&#8217;)  
and the following will not:  
CONNIP=$(/bin/ip addr | grep &#8216;inet 192.168.$NETWORK&#8217; | awk &#8216;{print $2;}&#8217;)

This was not what I was expecting especially when using backticks. The variables were not being interpolated.

[][1]

 [1]: http://www.linuxtopia.org/online_books/advanced_bash_scripting_guide/commandsub.html
