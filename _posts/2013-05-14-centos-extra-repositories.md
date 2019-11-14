---
tags: [Notebooks/itblog]
title: Centos Extra Repositories
created: '2019-09-29T11:18:05.398Z'
modified: '2019-10-18T14:22:56.036Z'
---

I use Centos a lot however it always seem to be missing the packages I need, unlike Debian which seems to have everything by default. In order to help do the following.

  * Enable the contrib repository &#8211; edit /etc/yum.repos.d/CentOS-Base.repo
  * Add RPMForge and EPEL repositories, details at [http://wiki.centos.org/AdditionalResources/Repositories][1]

Install RPMForge and EPEL on Centos 6:  

```
wget http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
sudo rpm -Uvh epel-release-6*.rpm
wget http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el6.rf.x86_64.rpm
rpm --import http://apt.sw.be/RPM-GPG-KEY.dag.txt
rpm -i rpmforge-release-0.5.2-2.el6.rf.*.rpm
```

[1]: http://wiki.centos.org/AdditionalResources/Repositories "http://wiki.centos.org/AdditionalResources/Repositories"
