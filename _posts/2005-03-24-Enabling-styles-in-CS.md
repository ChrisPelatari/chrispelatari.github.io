---
layout: post
title: Enabling styles in CS
---
[Straight from ScottW](http://www.communityserver.org/forums/465132/ShowPost.aspx), I added 

<pre><span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">MarkUp</span><span style="COLOR: blue">&gt;</span>
	<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">globalAttributes</span><span style="COLOR: blue">&gt;</span>
		<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">class</span> <span style="COLOR: red">enable </span>= "<span style="COLOR: blue">true</span>" /<span style="COLOR: blue">&gt;</span>
		<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">align</span> <span style="COLOR: red">enable </span>= "<span style="COLOR: blue">true</span>" /<span style="COLOR: blue">&gt;</span>
		<strong><span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">style</span> <span style="COLOR: red">enable </span>= "<span style="COLOR: blue">true</span>" /<span style="COLOR: blue">&gt;</span></strong>
		<span style="COLOR: blue">&lt;</span><span style="COLOR: maroon">id</span> <span style="COLOR: red">enable </span>= "<span style="COLOR: blue">true</span>" /<span style="COLOR: blue">&gt;</span>
	<span style="COLOR: blue">&lt;</span>/<span style="COLOR: maroon">globalAttributes</span><span style="COLOR: blue">&gt;</span></pre>
  
notice the style element? That cleared up the little non-formatted code issue 
that I had in my previous post.