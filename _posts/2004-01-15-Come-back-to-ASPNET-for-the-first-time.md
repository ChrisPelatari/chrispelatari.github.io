---
layout: post
title: Come back to ASP.NET for the first time.
---
<p>Today I had to bring up a previous project that I had done in asp.net and 
make sure that it would work well if installed to an end-user's machine for beta 
testing.</p>
<p>For the past several months, I've been doing development for in-house 
applications using WinForms, so it took an hour or two to get back into the 
asp.net groove. Once I said "oh yeah" a few times tho, I've got to say - I miss 
it. I even dusted off some old javascript skills (thanks to a <a href="http://www.julialermaninc.com/blog/PermaLink.aspx?guid=8299c061-1b16-4d1d-820a-40011c5e6c3b" target="_blank">little help from Julie</a>) and after updating one stored 
procedure to work with some new functionality, I've got a completely working 
test deployment in as close as an environment to the target as I could 
muster.</p>
<p>On that note - be careful using .msi technology and then trying to xcopy an 
updated .dll to the \bin of your web app in XP. Apparently, it won't let asp.net 
create an appdomain and you'll get the dreaded "Server Application Unavailable" 
error. Heh. Didn't see that one coming - when I test deployed to a Win2k 
workstation, I did not get the same error, it just worked. Weird. 
</p>