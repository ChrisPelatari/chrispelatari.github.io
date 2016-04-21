---
layout: post
title: BackgroundWorker.isRunning
date: 2006-02-11 18:38
author: chrispelatari
comments: true
categories: [csharp,winforms]
---

This is a private boolean member of the new [BackgroundWorker](http://msdn2.microsoft.com/en-us/library/system.componentmodel.backgroundworker.aspx) class in .NET 2.0. If it were public, perhaps there would be less questions
like [this one on the gotdotnet messageboards](http://www.gotdotnet.com/Community/MessageBoard/Thread.aspx?id=359244). I ran into a similar problem recently
and decided that instead of catching an exception when the [BackgroundWorker](http://msdn2.microsoft.com/en-us/library/system.componentmodel.backgroundworker.aspx) is running, I would emulate the isRunning member myself.
Since this is multithreaded by its nature, I decided to use a [lock object](http://www.mono-project.com/Coding_Guidelines#Locking_and_Threading) to control access to a static boolean member in the class that uses
the [BackgroundWorker](http://msdn2.microsoft.com/en-us/library/system.componentmodel.backgroundworker.aspx) component.

```csharp
static bool isRunningBgWorker = false;
static object lockObj = new object();

...

if (!isRunningBgWorker) {
	this.backgroundWorker1.RunWorkerAsync();
}
```

I check to see if it's running before even setting it off to do the work.

```csharp
private void backgroundWorker1_DoWork(object sender, DoWorkEventArgs e) {
	lock (lockObj) {
		isRunningBgWorker = true;
	}
```

The first thing that happens when the DoWork eventhandler is called and

```csharp
private void backgroundWorker1_RunWorkerCompleted(object sender, RunWorkerCompletedEventArgs e) {
...

	lock (lockObj) {
		isRunningBgWorker = false;
	}
}
```

the last thing when the work is completed: controlled access to the
isRunningBgWorker member. Hope this helps somebody else out there who is having
trouble with the [BackgroundWorker](http://msdn2.microsoft.com/en-us/library/system.componentmodel.backgroundworker.aspx) component.
