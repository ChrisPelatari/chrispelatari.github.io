---
layout: post
title: "Greasmonkey goodies; embrace and extend"
description: ""
category: 
tags: []
---
 

<p>Thanks to <a href="http://blog.dreamprojections.com/archive/2005/06/02/905.aspx">Alex</a>, I 
checked out a great application of <a href="http://greasemonkey.mozdev.org/index.html">Greasemonkey</a> - the <a href="http://www.arantius.com/article/arantius/gmail+delete+button/">Gmail 
Delete Button</a>.</p>
<p>Of course, I had to look at the 
script since it's just javascript and play with it to see if I could extend it a 
little bit.</p>
<p>As with most of my "embrace and 
extend" forays, it was just a simple change - I use a <em>lot</em> of labels in 
gmail, so when I'm reading via the web interface, I have some organization to 
the 50+ email lists I'm a member of. Every screen that has conversations listed 
on it has a delete button, including the search view, except for labels (until 
you hit the search mail button, but then the number of visible conversations 
goes from 50 to 20).</p>
<p>So, I popped open the "view frame 
info" context menu item from gmail and saw that the view querystring parameter 
for a label was tl. With that in mind:</p>
<p><pre><span style="COLOR: blue">if</span> (document.location.search) {
	<span style="COLOR: blue">if</span> (document.location.search.match(/search=inbox/)
		||
		document.location.search.match(/search=query/)
		||
		<strong>document.location.search.match(/view=tl/) &amp;&amp;
		!document.location.search.match(/search=trash/)</strong>
		||
		document.location.search.match(/view=cv/) &amp;&amp; 
		!document.location.search.match(/search=trash/)
	) {
		setInterval(<span style="COLOR: maroon">'try{window._gd_place_delete_buttons();}catch(e){}'</span>, <span style="COLOR: maroon">25</span>);
	}
}</pre></p>
<p>I'm not sure if the  &amp;&amp; 
!document.location... part that I added is necessary, but it doesn't hurt 
anything. Now I can delete posts in all of the views that I would want to in 
gmail.</p>