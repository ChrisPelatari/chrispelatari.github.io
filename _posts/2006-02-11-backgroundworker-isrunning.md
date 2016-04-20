---
layout: post
title: BackgroundWorker.isRunning
date: 2006-02-11 18:38
author: chrispelatari
comments: true
categories: [Uncategorized]
---

<p>This is a private boolean member of the new <a href="http://msdn2.microsoft.com/en-us/library/system.componentmodel.backgroundworker.aspx">BackgroundWorker 
</a>class in .NET 2.0. If it were public, perhaps there would be less questions 
like <a href="http://www.gotdotnet.com/Community/MessageBoard/Thread.aspx?id=359244">this 
one on the gotdotnet messageboards</a>. I ran into a similar problem recently 
and decided that instead of catching an exception when the <a href="http://msdn2.microsoft.com/en-us/library/system.componentmodel.backgroundworker.aspx">BackgroundWorker 
</a>is running, I would emulate the isRunning member myself.</p>
<p>Since this is multithreaded by its nature, I decided to use a <a href="http://www.mono-project.com/Coding_Guidelines#Locking_and_Threading">lock 
object </a>to control access to a static boolean member in the class that uses 
the <a href="http://msdn2.microsoft.com/en-us/library/system.componentmodel.backgroundworker.aspx">BackgroundWorker 
</a>component.</p><pre><span style="color:blue;">static</span> <span style="color:blue;">bool</span> isRunningBgWorker = <span style="color:maroon;">false</span>;
<span style="color:blue;">static</span> <span style="color:blue;">object</span> lockObj = <span style="color:blue;">new</span> <span style="color:blue;">object</span>();

...

<span style="color:blue;">if</span> (!isRunningBgWorker) {
	<span style="color:blue;">this</span>.backgroundWorker1.RunWorkerAsync();
}</pre>
<p>I check to see if it's running before even setting it off to do the work.</p><pre><span style="color:blue;">private</span> <span style="color:blue;">void</span> backgroundWorker1_DoWork(<span style="color:blue;">object</span> sender, DoWorkEventArgs e) {
	<span style="color:blue;">lock</span> (lockObj) {
		isRunningBgWorker = <span style="color:maroon;">true</span>;
	}</pre>
<p>The first thing that happens when the DoWork eventhandler is called and</p><pre><span style="color:blue;">private</span> <span style="color:blue;">void</span> backgroundWorker1_RunWorkerCompleted(<span style="color:blue;">object</span> sender, RunWorkerCompletedEventArgs e) {
...

	<span style="color:blue;">lock</span> (lockObj) {
		isRunningBgWorker = <span style="color:maroon;">false</span>;
	}
}</pre>
<p>the last thing when the work is completed: controlled access to the 
isRunningBgWorker member. Hope this helps somebody else out there who is having 
trouble with the <a href="http://msdn2.microsoft.com/en-us/library/system.componentmodel.backgroundworker.aspx">BackgroundWorker 
</a>component.</p>
