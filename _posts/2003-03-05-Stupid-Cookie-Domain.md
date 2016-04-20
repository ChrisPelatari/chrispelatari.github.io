---
layout: post
title: Stupid Cookie.Domain
---
I've spent about 1 1/2 hours trying to figure out why I couldn't get a persistent cookie set from codebehind in ASP.NET...I tried a lot of different things but of course not the correct solution. The domain. rrrrrrgh!

The worst part is that I sorted this out a few weeks ago, but since then it hasn't been a big issue, I've been letting the framework of each application handle the details of www.mydomain.net communicating with demo.mydomain.net.

Today I've been back on the originating app's side, making sure things are ready to get set, then I got all sweaty and whatnot about the 'cookie not being set properly', which was kind of true - my browser didn't think the code was coming from the same host. localhost != www.mydomain.com. There's my 'D'oh!' for the day.

btw, it works still (whew!:)