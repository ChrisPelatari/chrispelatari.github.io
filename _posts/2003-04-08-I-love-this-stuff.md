---
layout: post
title: I love this stuff.
---
As a developer, I consider myself more of a problem solver. One of my least favorite problems: Com Interop. I can't shake it. It seems that no matter how hard I try, all of my apps to date have included interop.

That said, it's kind of fun revisiting one of my first asp.net endeavors and trying to remember why I architected it so poorly. Oh yeah, I'm a programmer - and at the time it was written, I remember having to make a few changes from .net beta 2 to RTM. Added to the fact that the only readily available examples that I had were in asp.old, looking back at the code has made me realize just how much I've grown over this time.

I was trouble shooting a new application that someone else is writing based on my previous code and com interop. Probably not the best idea, but the point is gotten across. I think. The developer in question just asked me "Where do you get the knowledge of how to deal with the worker process?". Well, the short answer is messing with it. Sometimes the resources that you need when debugging are locked up by a worker process that still thinks it's debugging - so Kill it! I'm not up to date on the niceties of IIS 6 and the refinements of the worker process there, but the one that ships with v1.0.3705 is just well built. I can kill it in task manager and a new one pops right up!

&lt;/rant&gt;

red or green pill, you live and you learn.