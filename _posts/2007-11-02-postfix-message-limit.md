---
tags: [Notebooks/itblog]
title: Postfix message limit
created: '2019-09-29T11:18:03.248Z'
modified: '2019-10-18T14:22:56.469Z'
---

Today integrit was trying to send a message and postfix was giving the following error:

<pre>Nov  2 11:17:16 mail postfix/postdrop[15184]: warning: uid=0: Illegal seek
Nov  2 11:17:16 mail postfix/sendmail[15183]: fatal: root(0): queue file write error
</pre>

It turns out that postfix has a message size limit of 10mb.

<pre>postconf -d | grep message_size_limit</pre>

You can change it using the following:

<pre>postconf -e "message_size_limit = 20480000"</pre>

This cleared the error and enabled by 15mb integrit message to go through!
