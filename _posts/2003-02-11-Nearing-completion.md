---
layout: post
title: Nearing completion...
---
I'm getting to the clean-up phase of porting an asp.old project to .NET. It's about time! I finally tackled a problem I ran into with a vb6 component that was run thru VS.NET to be converted to VB.NET - I couldn't figure it out till I used a 'magik number' hard coded into part of my application. 1 based arrays. Why?! Why I say!?! I've always been accustomed to using 0-based arrays, and as I've stepped thru the code I've seen this behavior in some of the VB.NET arrays - they place an element into the element at 0 that says &lt;empty element used to adjust for 1 based array&gt;.

Well, in this case it didn't happen like that. Oh, well. Just one of those things I guess.