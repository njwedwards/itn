---
tags: [Notebooks/itblog]
title: Adjust exif date for images
created: '2019-09-29T11:18:04.636Z'
modified: '2019-10-18T14:33:09.936Z'
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
