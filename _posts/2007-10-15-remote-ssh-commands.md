---
title: Remote SSH Commands
author: nedwards
layout: post
categories:
  - Uncategorized
---
In order to use remote ssh commands:

`ssh  hostname remotecommandname `

A local script can be executed locally via:

`cat localscript | ssh hostname -T`

Reference:

<http://www.debian-administration.org/articles/507>
