---
tags: [Notebooks/itblog]
title: Default Apache Virtualhost
created: '2019-09-29T11:18:03.437Z'
modified: '2019-10-18T14:22:56.144Z'
---

I have been trying to tidy up the apache config on the servers at work and ran into an issue with trying to set a default virtualhost to answer queries that did not relate to any specific virtualhost. For example if you type in the ip address of the machine.

I finally found some help in the [Apache 1.3 documentation][1]:

Now I am running Debain so have put the default virtualhost in /etc/apache2/sites-enabled/000-default and this works correctly. As the file starts with 0 it should always be added into the configuration first and thus be the default.

 [1]: http://httpd.apache.org/docs/1.3/vhosts/name-based.html#using
