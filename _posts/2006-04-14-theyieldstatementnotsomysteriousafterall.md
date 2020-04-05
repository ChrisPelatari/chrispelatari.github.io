---
layout: post
title: the yield statement - not so mysterious after all?
date: 2006-04-14 15:13
author: chrispelatari
comments: true
categories: [professional_geek]
---

<blockquote>
  <p><font face="Tahoma"><strong>Using Yield in Practice<br /></strong></font><font face="Tahoma">The moral of the story is <em><font color="#ff0000">STOP thinking so 
  hard about it</font></em>, just use "yield return" the next piece of data in 
  the list.  When using the yield statment GetEnumerator's job is to answer 
  foreach's question - "what's my next item please".  Walk all the items in 
  your collection and yield return what you want.  Don't worry about 
  remembering where you were - that's all part of the generated statemachine goo 
  - it will stop and start the function you write as it pleases in it's MoveNext 
  implementation or whatever (cause we dont really care - we're not 
  suppposed to be thinking, remember?) .  =)</font><img height="1" src="http://blogs.msdn.com/aggbug.aspx?PostID=565559" width="1" /></p></blockquote>
<p><i>[Via <a href="http://blogs.msdn.com/jfoscoding/archive/2006/03/31/565559.aspx">jfo's 
coding</a>]</i> </p>
<p>I'll admit, I haven't thought a whole lot about yield because, well, I 
couldn't find anything that described what it did in terms I could understand. I 
just kept thinking "oh, cool, another new feature in .net 2.0 that I'll get to 
learn by the time 3.0 comes out" and moved on to the next task.</p>
<p>Thinking about it as kind of a "macro" (similar to what a using(){} block 
does) lets it gel a little better.</p>
