---
tags: [Notebooks/itblog]
title: Default shared folder permissions
created: '2019-09-29T11:18:05.567Z'
modified: '2019-10-18T14:22:56.166Z'
---

Set new files/folder to inherit the parent folder group

	sudo setgid g+s /home/folder

Recursively set new filer/folders to have 'rwx' set
	
	sudo setfacl -R -m d:g::rwx /home/folder
