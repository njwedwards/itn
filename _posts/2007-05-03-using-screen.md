---
title: Using Screen
author: nedwards
layout: post
categories:
  - Uncategorized
---
The unix program screen can be very helpful. Its good because the session that you are using will continue to run after you log off. This is especially useful if you are doing a download or running a command that takes a long time. Below are some common commands:

C-a n = next  
C-a p = previous  
C-a d = detach (exit)  
C-a c = new terminal  
C-a S = split the screen  
C-a : resize 20

From the command line:  
screen -ls  
screen -R (reattach)

Extra help [http://gentoo-wiki.com/TIP\_Using\_screen][1]

 [1]: http://gentoo-wiki.com/TIP_Using_screen
