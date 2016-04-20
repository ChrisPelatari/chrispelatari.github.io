---
layout: post
title: xsd2db and Me
---
>I have been looking for [xsd2db](http://sourceforge.net/projects/xsd2db/), a tool for generating a database schema from an XML schema, ever since I read [this article](http://radio.weblogs.com/0112946/stories/2003/04/29/unifyingObjectAndRelationalDataStructures.html).  Unfortunately, when it came time for me to recall the location of the tool I had forgotten where I found it in the first place (I'm sometimes lazy on my bookmarks).  Thanks to [Mike Gunderloy's](http://www.larkware.com/index.html) most recent [Daily Grind](http://www.larkware.com/Articles/TheDailyGrind85.html), I was able to locate the tool.

>It works as promised, and I was able to create a database with the appropriate entities for a few complex types defined in my XSD for a SQL Server database and an Access database. 

>\[[Chad Osgood's Blog](http://weblogs.asp.net/cosgood/posts/7660.aspx)\]

Schweet! I've been thinking about changing over the backend for my blog engine to use sql server since it's available to me, and it looks like I will now have the chance. Nice.

I used this tool to generate a SQL Server DB using the xsd that is currently in place. I'm still not sure if it will handle annotated datasets, but that's just a few keystrokes away I think. Cool deal - tools like this make things so much easier to deal with...for me anyway:)