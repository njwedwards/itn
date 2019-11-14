---
tags: [Notebooks/itblog]
title: LVM on iSCSI exported via Linux LVM
created: '2019-09-29T11:18:04.639Z'
modified: '2019-10-18T14:29:51.469Z'
---

I am running Openfiler 2.99 and exporting an LVM volume via iSCSI.

Recently I have been having an issue where, I have been seeing a duplication of volume group. Initially I thought this was some sort of issue with Openfiler. However it occurred because I had created another volume group on the server that was connecting to the exported volume. So the Openfiler host is seeing the LVM data on exported volume and getting confused, I guess this makes sense though.

I will need to careful with volume group names in the future in order not to get this issue again.
