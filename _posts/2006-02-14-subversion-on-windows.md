---
layout: post
title: Subversion on Windows
date: 2006-02-14 18:08
author: chrispelatari
comments: true
categories: [professional_geek]
---

<p>I've been wanting to setup <a href="http://subversion.tigris.org">subversion</a> for <a href="http://postxing.net">PostXING</a> for a while so I can have more 
control over who has commit access and various adminy tasks that are only 
available thru emailing the already busy staff of <a href="http://sourcegear.com">sourcegear</a> when hosting code on <a href="http://vaultpub.sourcegear.com">vaultpub</a>.</p>
<p>Thankfully, I'm not the only person who has had this idea. To that end, <a href="http://blogs.clearscreen.com/migs/archive/2005/01/21/824.aspx">this blog 
post </a>was instrumental in outlining the steps to take to get subversion up 
and running on a windows box. The only issue that I had which was rather 
annoying was I kept getting an error stating that svn was "unable to open an 
ra_local session to URL" when trying to import code on the host. So, I did 
things the painfully slow way of adding files/folders from a client machine that 
already had the code on it. The good news is that PostXING now has its own 
subversion repository: <a href="svn://postxing.net/PostXING">svn://postxing.net/PostXING</a> read 
access is still there for all, but now I can specify who can and cannot commit 
changes. So nice.</p>
