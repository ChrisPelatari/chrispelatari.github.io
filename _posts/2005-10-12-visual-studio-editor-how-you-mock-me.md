---
layout: post
title: Visual Studio Editor, how you mock me.
date: 2005-10-12 05:40
author: chrispelatari
comments: true
categories: [professional_geek]
---

<p>I've been chasing down this odd <a href="http://blogs.msdn.com/vseditor/archive/2005/05/12/417011.aspx">Visual 
Studio bug where the Enter, Backspace, and Arrow keys stop working.</a></p>
<p>It happened to me in Redmond at Microsoft Campus (of all places!) and it's a 
known bug that a lot of others have run into apparently. Some folks have noted 
that <a href="http://www.hanselman.com/blog/CommentView,guid,7d4b6fa8-85d8-4e3d-90d8-cb1d4e2966a2.aspx">it 
happens with the Beta 2 build</a>, but the link above claims that it is gone 
from later builds. Sorry, wrong answer, kimo-sabe. Even on the RC 
build, this showed up.</p>
<p>It has to do with how Visual Studio handles USER SETTINGS. Thanks to a 
comment in ScottH's blog, I found a command line switch (devenv /resetuserdata) 
that brought up a user settings dialog asking me to set a profile when I started 
Visual Studio again. Instead of my usual C# profile, I decided to go with the 
General profile to mimic VS2003's settings. And whaddaya know? I can actually 
edit source files (for now). This does not bode well for Visual Studio as a 
development environment. Things should work by default, right? I can 
envision answering many questions about this in forums which I am subscribed to. 
</p>
<p>Goodbye, past coupla days. I'll miss ya.</p>
