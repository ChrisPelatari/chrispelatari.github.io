---
layout: post
title: The logic (or lack thereof) behind xhtml:body
---
>When Sam started a small revolution last month by using [&lt;xhtml:body&gt; ](http://www.intertwingly.net/blog/1299.html) in his rss-feed, &lt;snip/&gt;

>On top of that, it seems like every rss feed that uses xhtml:body, uses tags like &lt;body xmlns="http://www.w3.org/1999/xhtml"&gt; for every item ,

>&lt;snip/&gt;

>\[[Luke Hutteman's Weblog](http://www.hutteman.com/weblog/2003/04/23.html#000074)\]

So am I missing something, or would an RSS feed be considered valid xhtml if using the &lt;body&gt; element in its items collection? As I'm typing this I'm thinking no - no &lt;html&gt; element, yadda yadda...

Okay, then - some more research is in order then. Two items - a filter for xhtml, and a way for extensible comments to bake in to the infiniblog. I've been looking thru some other's ideas on a [CommentAPI](http://wellformedweb.org/story/9), but I'm not sure how I should implement it - if what I'm thinking is true, an aspx page which uses a server-side form won't accept a POST from an outside script. I could use a webservice, but what about an .ashx?

The xhtml filter will require a bit more insight as to how HttpHandlers/HttpModules are handled in the runtime. We are implementing the rss feed thru an HttpHandler that accepts requests for .rss files. (We, well - [Chris Hollander](http://objective.mine.nu/) and my hi-jacking of his code:) So I need to find out if the HttpModules are still called when a Handler is implemented. Haven't really checked out the TraceLog yet.

Okay, enough blabbing - time to find out. cya!