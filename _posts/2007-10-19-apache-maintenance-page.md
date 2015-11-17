---
title: Apache maintenance page
author: nedwards
layout: post
categories:
  - Uncategorized
---
In order to put up a page during website downtime use mod_rewrite with:

`<br />
        ### To be uncommented to display maintenance page<br />
        RewriteCond %{REQUEST_URI} !/maint.html$<br />
        RewriteCond %{REQUEST_URI} !/logo.png$<br />
        RewriteRule ^(.*) /maint.html<br />
   `
