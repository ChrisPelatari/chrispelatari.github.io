---
layout: post
title: Local DasBlog
---
<p>Wow. I realized that I needed some guidance on how to implement the MetaWeblog API and thought, hmm, doesn't that dasBlog jobby do cross-posting with that (api)? Ah, so it does. Ah, and there is some source code to go along with that, thank you.</p>
<p>It doesn't look like I'll be doing anything really “ground-breaking” or “innovative” with my new side project...I'll really just be hacking a few disparate parts together to achieve a goal that I have - and learn more about what I can do with Windows Forms while I'm at it. That's okay with me. </p>
<p>In other news, I finally made use of those commented out settings in my local blog.config for .Text, [host] and [application]. The comment preceding that says, “It is possible to mirror a blog and hard code a specific Host and Application”. Right. I first read this and said, okay, that sounds great. But, what would I use it for? </p>
<p>I've found that setting these two elements lets me run .Text locally, but using the values that the server in question has for its application and host values. So, while I see “http:localhost/dottextweb” the .Text engine sees “http:myinternalserver/thatblog”. Sweet.<img width="0" height="0" src="http://localhost/DasBlog/cptrk.ashx?id=7b6c8700-a11f-400b-84d8-b6b62f302d47" /></p>