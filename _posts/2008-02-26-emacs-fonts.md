---
title: Emacs fonts
author: nedwards
layout: post
categories:
  - Uncategorized
---
If like me you use emacs the default fonts are not that great.

Just use the following, condensed from <http://peadrop.com/blog/2007/01/06/pretty-emacs/>

Add the following to /etc/apt/sources.list:  
`deb     http://ppa.launchpad.net/avassalotti/ubuntu feisty main<br />
deb-src http://ppa.launchpad.net/avassalotti/ubuntu feisty main`

Then run:  
`sudo aptitude update<br />
sudo aptitude install emacs-snapshot-gtk`

Now run (You can use a different size font like Monospace-10 if needed):  
`echo "Emacs.font: Monospace-9" >> ~/.Xresources<br />
xrdb -merge ~/.Xresources`

Now start emacs with:

`emacs-snapshot-gtk`
