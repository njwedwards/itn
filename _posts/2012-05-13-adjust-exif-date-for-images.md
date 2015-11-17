---
title: Adjust exif date for images
author: nedwards
layout: post
tagazine-media:
  - 'a:7:{s:7:"primary";s:0:"";s:6:"images";a:0:{}s:6:"videos";a:0:{}s:11:"image_count";s:1:"0";s:6:"author";s:6:"606253";s:7:"blog_id";s:6:"846587";s:9:"mod_stamp";s:19:"2012-05-13 13:13:08";}'
categories:
  - Uncategorized
tags:
  - photos
---
Sometime the date/time is wrong on jpg images. To adjust use exiv2.

show exif data:  
\# exiv2 pr img_0343.jpg  
go back an hour  
\# exiv2 ad -a -01:00:00 img_03*  
add a month  
\# exiv2 ad -O 1 img_03*  
add a day  
\# exiv2 ad -D 1 img_03*
