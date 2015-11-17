---
title: Add mirror to cpan
author: nedwards
layout: post
categories:
  - Linux
  - Perl
---
Quite often I come across a cpan install where there is no cpan mirror defined or it is defined as an ftp site the the firewall allows only http traffic.

Use the following to add a mirror:

`o conf urllist push "http://www.cpan.org"`

Now reload the index and save the changes:

`reload index<br />
o conf commit`
