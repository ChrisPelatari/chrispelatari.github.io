---
layout: post
title: Visual Studio 2005 Designer&#58; Touchy, Thouchy!
date: 2006-03-31 02:55
author: chrispelatari
comments: true
categories: [Uncategorized]
---

<p>If you do anything "out of the ordinary" in your UserControl or Form derived
classes in Visual Studio 2005, let me introduce you to a little snippet that
will probably save you lots of headaches:</p><pre><span style="color:blue;">if</span> ( DesignMode ) <span style="color:blue;">return</span>;</pre>
<p>or, its equally useful counterpart</p><pre><span style="color:blue;">if</span>(!DesignMode){
	doStuff();
}</pre>
<p>Now, the "out of the ordinary" thing I was doing was...hooking up an instance
EventHandler using a static property that exposes a Form derived class in an
OnLoad override. What? I know, not the clearest situation, and probably one that
could use a boatload of refactoring, but it works. In short, if you are having
designer problems in Visual Studio 2005, it may be worth it to sit back for a
bit and think about what introduced the designer error. Prime candidates are
constructors and OnLoad overrides that use static methods for functionality.
This code didn't allow me to view the designer of a
<em>different </em>form:</p><pre><span style="color:blue;">public</span> <span style="color:blue;">override void</span> OnLoad(EventArgs e){
	AppManager.ConcreteEditorForm.NewPostCreated += <span style="color:blue;">new</span> EventHandler(HandleNewPost);
}</pre>
<p>while this one would:</p><pre><span style="color:blue;">public</span> <span style="color:blue;">override</span> <span style="color:blue;">void</span> OnLoad(EventArgs e){
	<span style="color:blue;">if</span>( DesignMode ) <span style="color:blue;">return</span>;
	AppManager...
}</pre>
