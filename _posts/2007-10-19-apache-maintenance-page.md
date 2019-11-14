---
tags: [Notebooks/itblog]
title: Apache maintenance page
created: '2019-09-29T11:18:02.452Z'
modified: '2019-10-18T14:22:55.966Z'
---

In order to put up a page during website downtime use mod_rewrite with:

`<br />
        ### To be uncommented to display maintenance page<br />
        RewriteCond %{REQUEST_URI} !/maint.html$<br />
        RewriteCond %{REQUEST_URI} !/logo.png$<br />
        RewriteRule ^(.*) /maint.html<br />
   `
