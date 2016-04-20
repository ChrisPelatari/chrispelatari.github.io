---
layout: post
title: Exposing Hidden Events
date: 2007-04-25 17:44
author: chrispelatari
comments: true
categories: [Uncategorized]
---

<p>I recently ran into a neat little nugget of functionality in C# with events. 
Normally in C# when we define events we stop at something like this:</p><pre><span style="color:blue;">public</span> <span style="color:blue;">event</span> EventHandler&lt;MyEventArgs&gt; MyEvent;</pre>
<p>The thing is, you can explicitly implement the add and remove accessors if 
you throw some curly braces into the mix. Why does this matter? Imagine that you 
have a MainForm, and a usercontrol named ControlPanel. ControlPanel 
contains another usercontrol called hiddenControl that exposes an event that you 
want to handle in MainForm, but all MainForm has access to is 
ControlPanel...</p><pre><span style="color:blue;">public</span> <span style="color:blue;">event</span> <font color="#92dceb">EventHandler</font>&lt;<font color="#92dceb">MyEventArgs</font>&gt; MyEvent{
	<font color="#0000ff">add</font>{
		<span style="color:blue;">this</span>.hiddenControl.MyEvent += <font color="#0000ff">value</font>;
	}
	<font color="#0000ff">remove</font>{
		<span style="color:blue;">this</span>.hiddenControl.MyEvent -= <font color="#0000ff">value</font>;
	}
}</pre>
<p>Now you can subscribe to the event in MainForm without making the usercontrol 
member public in ControlPanel.</p>
<p class="media">[ Currently Playing : Burn Away - Foo Fighters - One by One 
(4:57) ]</p>
