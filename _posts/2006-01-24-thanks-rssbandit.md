---
layout: post
title: Thanks, RssBandit.
date: 2006-01-24 08:21
author: chrispelatari
comments: true
categories: [Uncategorized]
---

<p><a href="http://rssbandit.org">RssBandit</a> has been a big inspiration for 
some of the specific features of <a href="http://postxing.net">PostXING</a>. As 
a matter of fact, where possible I've used code from RssBandit directly. At 
least half of proxy support, most of the plugin loading logic, and most recently 
(like you don't have it unless you monitor the branches for postxing) a 
little-used, very useful interface: IMessageFilter.</p>
<p>IMessageFilter is only implemented by the splitter control in the framework 
(according to reflector) but was extremely helpful in the quest to better handle 
the keyboard. There is only one method defined on the interface:</p><pre><span style="color:green;">//CF: thanks, rssbandit :)
</span><span style="color:blue;">public</span> <span style="color:blue;">bool</span> PreFilterMessage(<span style="color:blue;">ref</span> Message m) {</pre>
<p>The code then looks for the WM_KEYDOWN or WM_SYSKEYDOWN messages and handles 
things according to whatever rules you put in there. To get it hooked up, I 
simply overrode OnActivate and OnDeactivate and added 
Application.Add/RemoveMessageFilter(this);</p>
<p>I figured if I already posted the problem, I might as well post a solution as 
well. This was really helpful to the flat spot that was forming on my forehead, 
so thanks again RssBandit.</p>
