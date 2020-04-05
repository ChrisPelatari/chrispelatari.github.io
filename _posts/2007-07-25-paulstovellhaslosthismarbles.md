---
layout: post
title: Paul Stovell has lost his marbles.
date: 2007-07-25 04:35
author: chrispelatari
comments: true
categories: [professional_geek]
---
[note: this started as a comment but started getting a little long-winded. what follows is a little gentle ribbing of Paul for <a href="http://www.paulstovell.net/blog/index.php/runtime-caching/">a recent post he wrote about being a lazy cache programmer </a>:P]

Mr. Stovell, you've officially lost your marbles :P j/k

okay, just to play devil's advocate...&gt;:) I think the asp.net cache framework fits very nicely for its purpose - what you propose seems like another abstraction on top of it, for the benefit of thinking *less* about what items you should cache to *optimize* code execution time? So, just throw everything possible at it. Cache can handle that, right? hehe. nope. That's why you think about it, apply it where appropriate, and don't waste cycles calculating if you should even cache or not as part of the caching process of a production site. I dunno, seems like a wasted effort to me, especially when you start to go down the rabbit hole of deciding what should/shouldn't be cached as part of the process.

I'm not posting this to be a jerk...I'm putting your feet to the fire a little! Think it thru a little more, maybe (since I seem to be concentrating on the calculations as part of the process) move that logic outside of the [Deterministic] control flow to an external "cache minder" process. have your cake and cache it too.
<a href="http://chrispelatari.files.wordpress.com/2007/07/wheredacacheat.jpg"><img class="alignnone size-full wp-image-1140" alt="wheredacacheat" src="http://chrispelatari.files.wordpress.com/2007/07/wheredacacheat.jpg" width="120" height="90" /></a> but the main point of cache in asp.net is to improve performance by taking anything that takes longer than O(1) and returning it nearly that fast (a guess considering that Cache exposes itself as a Dictionary to store its items) I guess that means my case (while I'm advocating;) is for using the cache as is, and make conscious decisions on what should go into it instead of letting some attribute-fu decide for me. What happens when your attribute logic is wrong? DOOM! :P hehe, not really. What do you think?

p.s. my server crapped before I had a chance to post this. Is there some new law that states that technology starts to break down the minute you start to be a smart-ass?
