---
title: Convert Virtualbox disk (.vdi) to VMware disk (.vmdk)
author: nedwards
layout: post
categories:
  - Virtualisation
---
I needed to do this recently and found that the instructions on the net that told me to just use qemu did not work as the hard disk would not boot.

Then I found the following set of commands:

`VBoxManage internalcommands converttoraw vb.vdi vb.raw && qemu-img convert -O vmdk vb.raw vb.vmdk && rm vb.raw`

It worked at treat and I was up and running on VMware 2 Server.

<http://www.commandlinefu.com/commands/view/3773/convert-vdi-to-vmdk-virtualbox-hard-disk-conversion-to-vmware-hard-disk-format>
