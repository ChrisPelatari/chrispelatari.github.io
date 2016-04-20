---
layout: post
title: "PostXING and interfaces"
description: ""
category: 
tags: []
---
<p>I feel like I'm going nuts with interfaces in the next version of <a href="http://PostXING.url123.com/main">PostXING</a>. Interfaces are a language 
feature that is really powerful - you don't really start to appreciate it until 
you are faced with situations that would otherwise be impossible to deal 
with.</p>
<p>PostXING already uses interfaces to load plugins like the <a href="http://PostXING.url123.com/nsv1.0.5005.1">NetSpellPlugin </a>for spell 
checking. So I thought hey, go with what you know for this plugin/provider idea 
that I've had stewing in my head for a while. I've already included <a href="http://mikedub.net/">MikeDub's </a>awesome <a href="http://url123.com/a2nq7">IUI library</a> (modified with - you guessed 
it, <a href="http://www.chrisfrazier.net/blog/archive/2004/09/11/593.aspx">interfaces</a>!) 
so I figured I might as well milk that for all it's worth. And trust me, I am 
:)</p>
<p>The idea I have is to use IUI to set up a new/edit an existing "blog" (what 
PostXING sees as a blog) and let each plugin/provider take care of any special 
configuration they might need. But there's a problem - every provider should 
have common attributes defined within the interface, but there is also non-blog 
information that I would like to store (like ftp settings, whether or not you 
want media information to show up like below (I know, Alice in Chains again - I 
just write good code to that CD), and preview formatting). </p>
<p>So, how do I communicate that the custom IUI pages are done so that the rest 
of the configuration can continue? Well, I <em>could</em> use a vanilla 
EventHandler event, but how can I make sure that the main exe project will be 
able to handle the event without knowing which provider has been loaded? 
Furthermore, how can the provider send up an event for it to catch without 
having a reference to the main exe project (a circular dependency - nono!)?</p>
<p>Interfaces.</p>
<p>I create an interface that only the dialog that shows the configuration pages 
should implement. It could be a simple interface with only 1 to 3 methods 
defined for it (if I want to only expose moving forward to one page vs. moving 
to any available page thereafter)...see what I'm getting at? Maybe some code 
will better explain what I'm getting at:</p>
<p><pre><span style="COLOR: blue">using</span> System;
<span style="COLOR: blue">using</span> System.Collections;

<span style="COLOR: blue">public</span> <span style="COLOR: blue">interface</span> IFoo{
	<span style="COLOR: blue">void</span> HandleEvent(<span style="COLOR: blue">object</span> sender, EventArgs e);
}

<span style="COLOR: blue">public</span> <span style="COLOR: blue">class</span> FooInstance : IFoo{
	<span style="COLOR: blue">public</span> <span style="COLOR: blue">void</span> HandleEvent(<span style="COLOR: blue">object</span> sender, EventArgs e){
		System.Windows.Forms.MessageBox.Show(<span style="COLOR: maroon">"Handled! Booyakasha!"</span>);
	}
}

<span style="COLOR: blue">public</span> <span style="COLOR: blue">class</span> MyClass
{
	<span style="COLOR: blue">public</span> <span style="COLOR: blue">static</span> <span style="COLOR: blue">void</span> Main()
	{
		IFoo thisfoo = <span style="COLOR: blue">new</span> FooInstance();
		
		MyClass s = <span style="COLOR: blue">new</span> MyClass();
		
		s.WireUpEvent(thisfoo);
		
		<span style="COLOR: blue">if</span>(s.throwevent != <span style="COLOR: blue">null</span>){
			s.throwevent(s, EventArgs.Empty);
		}
	}
	<span style="COLOR: blue">public</span> <span style="COLOR: blue">event</span> EventHandler throwevent;
	
	<span style="COLOR: blue">public</span> <span style="COLOR: blue">void</span> WireUpEvent(IFoo foo){
		<span style="COLOR: blue">this</span>.throwevent += <span style="COLOR: blue">new</span> EventHandler(foo.HandleEvent);
	}
}</pre></p>
<p>This was a little POC that I coded up in snippet compiler - and yes, it 
compiles and runs wonderfully. Booyakasha indeed. Here, IFoo is the interface 
that is implemented by the dialog. Passing the concrete FooInstance (the dialog) 
to the method WireUpEvent of what will be the provider class works thanks to 
wonderful, wonderful interfaces.</p>
<p class="media">[ Currently Playing : Nutshell - Alice in Chains - Unplugged 
(4:57) ]</p>