---
tags: [Notebooks/itblog]
title: Install Tomcat 6 on Debian Lenny with pinning
created: '2019-09-29T11:18:04.252Z'
modified: '2019-10-18T14:32:36.667Z'
---

I recently needed to install tomcat 6 on debian lenny, however it is not in the repository and there is no backport.

There were two options, either use the tar or install the debian testing package. I have opted for the testing package as it is a debian specific setup and integrates properly.

I am assuming that you already have the debian java 6 package installed. Run the following as root.

First set the release to stable:  
`<br />
echo 'APT::Default-Release "stable";' > /etc/apt/apt.conf<br />
`  
This is important and not setting this will cause issues.

Now add the testing repository:  
`<br />
cat <<EOF>/etc/apt/sources.list.d/squeeze.list<br />
# Repository for Squeeze, to get Tomcat6<br />
deb http://ftp.uk.debian.org/debian squeeze main contrib non-free<br />
deb-src http://ftp.uk.debian.org/debian squeeze main contrib non-free<br />
EOF<br />
`

Now pin the new packages:  
`<br />
cat <<EOF>/etc/apt/preferences<br />
Package: *<br />
Pin: release o=Debian,a=stable<br />
Pin-Priority: 990<br />
Package: *<br />
Pin: release o=Debian,a=testing<br />
Pin-Priority: 500<br />
Package: tomcat6,tomcat6-admin,tomcat6-common,libtomcat6-java,libservlet2.5-java<br />
Pin: release o=Debian,a=testing<br />
Pin-Priority: 990<br />
EOF<br />
`

The above with ensure that testing packages will only take the priority for the tomcat related packages. The higher pin priority takes precedence.

Now update the repositories and install tomcat 6.  
`<br />
aptitude update<br />
aptitude install tomcat6<br />
`

Ref:

<http://www.waltercedric.com/component/content/article/193-technical/1634-debian-lenny-how-to.html>  
[Why no apt-pinning by release name?][1]  
[http://www.debian.org/doc/manuals/debian-reference/ch02.en.html#\_tweaking\_candidate_version][2]

 [1]: http://linux.derkeiler.com/Mailing-Lists/Debian/2008-12/msg01207.html
 [2]: http://www.debian.org/doc/manuals/debian-reference/ch02.en.html#_tweaking_candidate_version
