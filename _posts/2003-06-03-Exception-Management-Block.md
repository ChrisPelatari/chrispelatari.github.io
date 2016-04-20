---
layout: post
title: Exception Management Block
---
Okay, so I dove into the [Exception Management Application Block today](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/dnbda/html/emab-rm.asp). 

I've been using it on a current application, but I wanted an email to be sent to me on an exception, so I had to subclass. So far, the EventLog has been enough.

I found a little quirk that I suppose I should have realized before - the default ASPNET user does not have rights to create an EventLog section for custom viewing of application exceptions, so the section I was trying to create just wasn't kickin it. This was a bit tough to find, as the QuickStart that comes with the application block creates the section no problem (if you have admin rights like me;)

Basically, all I had to do to get the custom "Publisher" to work was to remove the logName="" and applicationName="" elements from the configuration section of web.config. Now I get the EventLog and Email notification - and only one half of my head retains the dent from this morning's banging.