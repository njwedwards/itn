---
tags: [Notebooks/itblog]
title: Disable Ldap Users
created: '2019-09-29T11:18:02.451Z'
modified: '2019-10-18T14:22:56.191Z'
---

I have been trying to find out how to disable system users when the system is using ldap for authentication. Of course you can delete the user or change the password, but I was looking for a way to just disable which will give the opportunity to enable again later without knowing the password.

It turns out that you can disable a user in a similar what to what you do when a user is in the /etc/shadow file. Just add a ! after the {crypt} as follows:

{crypt}!$1$V6Nc9jxQ$KiOfSRRdS2DvJ.aDWkoRQ1

I have recently found [LAT][1] (Ldap Administration Tool). It seems to work really well.

 [1]: http://dev.mmgsecurity.com/projects/lat/
