---
layout: post
title: ReverseDOS Configuration for CS::Blogs revisited
date: 2005-07-02 00:24
author: chrispelatari
comments: true
categories: [professional_geek]
---
<p>I just set up CS::Blogs 1.1 on my server <a href="/blog">over here</a> and I wanted to keep 
ReverseDOS going for it. So I just copied over the settings from my web.config 
and thought I would be gold...not so, grasshopper.</p>
<p>The new section in the default web.config is now named 
<strong><u>memberrolesprototype</u></strong> so if you want to upgrade and 
not have to pull your hair out, keep this in mind.</p>
<p><font color="red">update</font>:</p><pre>	<span style="color:blue;">&lt;</span><span style="color:maroon;">memberrolesprototype</span><span style="color:blue;">&gt;</span>
		<span style="color:blue;">&lt;</span><span style="color:maroon;">ReverseDOS</span><span style="color:blue;">&gt;</span>
			<span style="color:blue;">&lt;</span><span style="color:maroon;">settings</span> <span style="color:red;">enabled</span>="<span style="color:dodgerblue;">true</span>" <span style="color:red;">debugEnabled</span>="<span style="color:dodgerblue;">false</span>" <span style="color:red;">debugKey="oink</span>=225678" <span style="color:red;">hideExceptions</span>="<span style="color:dodgerblue;">true</span>" /<span style="color:blue;">&gt;</span></pre>
<p class="media">[ Currently Playing : The World Has Turned and Left - Weezer - 
Weezer (Blue Album) (4:18) ]</p>
