---
layout: post
title: ypXmlTree
---
I'm still kicking around some ideas for an online aggregator, so I can maybe look over some of the blogs I frequent over my loverly dial-up connextion at home. I wanted to use a tree structure like the left pane of [SharpReader](http://www.sharpreader.net/) (and others, but sharpreader's what I use a lot:).

In my searching, I found a great xml tree component from [youngpup](http://www.youngpup.net/). Well, I've had my hands on it for a while, but I'm just now getting to the meat of it. This component uses xslt to convert an xml file to html, then uses javascript to toggle expanded state. Good component, but there's a little snafu.

I want to take an opml file (generated from sharpreader) and use it to populate my tree. This means I can either a) apply xslt to the opml file so it will retain the structure needed for the javascript component or b) write a custom server control that will take opml and generate the necessary html for the javascript.

Not sure which way I'm gonna go at this point, but I'm leaning toward b as I have experience with server control authoring and zilch with xslt. Might be fun to learn xslt, but I think that I may leave that route to a later date and a more seasoned developer.