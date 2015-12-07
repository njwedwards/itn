---
title: Default shared folder permissions
author: nedwards
layout: post
published: true
---


# Default permisions for shared folder

Set new files/folder to inherit the parent folder group

	sudo setgid g+s /home/folder

Recursively set new filer/folders to have 'rwx' set
	
	sudo setfacl -R -m d:g::rwx /home/folder
