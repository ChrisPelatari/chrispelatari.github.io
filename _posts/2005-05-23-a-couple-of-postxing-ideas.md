---
layout: post
title: "A couple of PostXING ideas"
---
 
<p>Thanks to <a href="http://weblogs.asp.net/wallym">Sir Wally</a> for the first 
one...it's simple really, Wally just asked if I would cache a list of the 
categories for each configured blog to aid with offline posting. I pretty much 
always use <a href="http://PostXING.url123.com/main">PostXING </a>while online, 
so this particular feature didn't even cross my mind. As a side effect, this 
will let me add categories to posts off of my CS blog which gives a nice little 
error when I try to get the comments list currently. Good one, Wally.</p>
<p>The other thing is that I want to expand the abilities of <em>where</em> 
PostXING can post - not just using the Metablog API, but being able to use 
different services. I don't want to use the "provider model" because I 
don't think that particular pattern fits what I have in my head to make 
this work. Close, as a matter of fact, very close, but not exactly what I'm 
looking for.</p>
<p>The basic idea that I have now is based on the fact that a lot of the 
functionality that PostXING uses now already sits in separate dll's in the 
application root. I think that I can factor out the API specific functionality 
into kind of a plugin - thereby expanding the end applications that can be 
posted to from PostXING. I haven't hashed out all of the details yet. This is 
still a brainstorm at this point. However it works out, it's going to be a major 
version change. </p>
<p>If this can work out the way I think it can, this could be a very cool 
addition to PostXING. Very cool indeed.</p>