---
layout: post
title: BradA at the Houston .NET UG
---
Although he only talked about high-level stuff (Exception Handling and Memory 
Management), I think Brad did a pretty good job. I stopped going to the 
Microsoft office out here because of all the <a href="http://support.microsoft.com/?scid=http://support.microsoft.com%2Fservicedesks%2Fwebcasts%2Flevels.asp">100 
level</a> classes, I couldn't justify taking time out of the trenches for 
learning stuff I already knew. But hearing the lead PM on the CLR team speak? It 
was time to attend my first <a href="http://hdnug.org/hdnug/home.aspx">Houston 
.NET UG</a> meeting. To be fair, there was also the <a href="http://www.hal-pc.org/~odiswooten/csharp/">Hal-PC C# sig</a> there, but 
I've never seen that room so packed. Overflow rooms had to be set up. Way to go, 
Brad!

So as is usually the case with these events, I came away with a couple of 
golden nuggets of information, some of which is even relevant in v1.x of the 
framework! (Imagine that!) Here are a couple of the notes I took:

* Finalizers keep objects alive an order of magnitude (about 10) longer than objects w/o finalizers 
* It's a <strong><em>really</em></strong> bad idea to throw an Exception from a finalizer. 
* <a href="http://blogs.msdn.com/cbrumme/archive/2004/02/20/77460.aspx">Check out Critical Finalizers in v2.0</a> 
* Finalizers are most appropriate for owned unmanaged resources (filestream, sqlconnection, etc classes are a case in point) 
* It's kind of an "unwritten rule" that any object that has a Close method should implement the IDisposable pattern and they should do the exact same thing. i.e. Close <u>should</u> just call Dispose.

I brought my digital camera, but being the jerk that I am, didn't check to 
see if the batteries were working first (doh!). Thankfully, I've got a camera 
phone and was able to take a picture with Brad anyways (I'm the short one):

<img src="/assets/images/02-16-05_1936.JPG" />

This is also where I got my <a href="http://www.chrisfrazier.net/Blog/archive/2005/02/16/724.aspx">Channel 9 guy</a> along with a nice smattering of other cool swag. Sorry, <a href="http://radio.weblogs.com/0001011/">Scoble</a>, it was just a joke tho - I 
thought it would be more appropriate to write the ransom note in 1337 than have 
both of my subscribers download a bunch of newspaper-clipped letter images. I 
still want my million, tho :)

<p class="media">[ Currently Playing : Napoleon 
Solo - At the Drive-In - In Casino Out (4:47) ]</p>