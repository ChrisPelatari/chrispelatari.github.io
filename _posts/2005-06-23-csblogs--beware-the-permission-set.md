---
layout: post
title: "CS::Blogs : beware the permission set"
description: ""
category: 
tags: []
---
<p>So I got some feedback about <a href="http://PostXING.url123.com/main">PostXING</a> saying that someone who 
had setup multiple blogs with <a href="http://communityserver.org">CS::Blogs</a> was getting the wrong blog 
back while trying to communicate with the Metaweblog API.</p>
<p>After a couple of questions, it turns out that all of the users were set up 
as sysadmins in the CS permission set, so anyone making a request to the 
metablog api would get a list of all the blogs available. Since PostXING 
ignorantly just uses BlogInfo[0] from the metablog_getUsersBlogs() method, 
everybody was trying to post to the first blog returned in the list.</p>
<p>So if you are running a multiple blog setup and wish to use the metablog api, 
make sure that your permissions are set so that when a user makes a request into 
his/her blog, theirs is the only blog they get back.</p>
<p>Thanks, <a href="http://cs.thycotic.net/blogs/jeff_schoolcraft/">Jeff.</a></p>
<p class="media">[ Currently Playing : Voodoo Child (Slight Return) - Jimi Hendrix 
- (5:12) ]</p>