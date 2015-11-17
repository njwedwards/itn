---
title: Sending email from Linux system to relay host
author: nedwards
layout: post
categories:
  - Email
tags:
  - email
---
The default install in Centos/RHEL and Debian seems to be to install Exim or Postfix. For what I usually need and that is just sending root email to my email address, this is too much. Also it can frustrating trying to get the &#8216;FROM&#8217; address to be correct.

ESMTP comes in very handy here. It will just send email on to your relay server and allow you to change the domain where the email comes from.

[Setting up on Centos][1]

[Set from address per user][2]

 [1]: http://www.how2centos.com/installing-ssmtp-on-centos-5-6/ "http://www.how2centos.com/installing-ssmtp-on-centos-5-6/"
 [2]: http://serverfault.com/questions/221696/ssmtp-change-from-root-xycom-root-name "http://serverfault.com/questions/221696/ssmtp-change-from-root-xycom-root-name"
