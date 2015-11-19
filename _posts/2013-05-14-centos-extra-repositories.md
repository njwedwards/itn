---
title: Centos Extra Repositories
author: nedwards
layout: post
categories: 
  - Linux
published: true
---

I use Centos a lot however it always seem to be missing the packages I need, unlike Debian which seems to have everything by default. In order to help do the following.

  * Enable the contrib repository &#8211; edit /etc/yum.repos.d/CentOS-Base.repo
  * Add RPMForge and EPEL repositories, details at [http://wiki.centos.org/AdditionalResources/Repositories][1]

Install RPMForge and EPEL on Centos 6:  

```
wget http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm<br />
sudo rpm -Uvh epel-release-6*.rpm<br />
wget http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el6.rf.x86_64.rpm<br />
rpm --import http://apt.sw.be/RPM-GPG-KEY.dag.txt<br />
rpm -i rpmforge-release-0.5.2-2.el6.rf.*.rpm
```

[1]: http://wiki.centos.org/AdditionalResources/Repositories "http://wiki.centos.org/AdditionalResources/Repositories"
