---
tags: [Notebooks/itblog]
title: Command history autocompletion
created: '2019-09-29T11:18:02.277Z'
modified: '2019-10-18T14:22:56.083Z'
---

Having used Gentoo quite a bit in the past, I had got used to using PageUp and PageDown to auto complete commands stored in your ./bash_history file. Well using Ubuntu and other distributions this did not seem to work.

Today I found out that you can enable this by adding the following to your /etc/inputrc:

“e[5~”: history-search-backward  
“e[6~”: history-search-forward

This will let you type the start of the command and then type PageUp or PageDown to offer you the matches from your command history. Its also worth changing HISTSIZE to something higher in your ./bash_profile.
