---
layout: post
title: Error&#58; Could not open the requested SVN filesystem
date: 2008-02-20 16:46
author: chrispelatari
comments: true
categories: [subversion,svn,apache]
---
When trying to connect to a new subversion repository over apache 2.0 using subversion 1.4.5. Error number:165005
Looked at the error log for apache, and saw this:

```
[Wed Feb 20 14:00:15 2008] [error] [client 192.168.xxx] (20014)Error string not specified yet: Expected format '3' of repository; found format '5'   
[Wed Feb 20 14:00:15 2008] [error] [client 192.168.xxx] Could not fetch resource information.  [500, #0]    
[Wed Feb 20 14:00:15 2008] [error] [client 192.168.xxx] Could not open the requested SVN filesystem  [500, #165005]
```

and then found where the subversion modules lived in httpd.conf:

```
LoadModule dav_svn_module modules/mod_dav_svn.so   
LoadModule authz_svn_module modules/mod_authz_svn.so
```

stopped apache, copied the two .so files from subversionbin to apache2modules and restarted Apache.

then holla'd w00t! XD
