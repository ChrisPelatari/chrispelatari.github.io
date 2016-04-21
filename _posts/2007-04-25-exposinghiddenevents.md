---
layout: post
title: Exposing Hidden Events
date: 2007-04-25 17:44
author: chrispelatari
comments: true
categories: [dotnet,winforms,csharp]
---

I recently ran into a neat little nugget of functionality in C# with events.
Normally in C# when we define events we stop at something like this:

```csharp
public event EventHandler<MyEventArgs> MyEvent;
```

The thing is, you can explicitly implement the add and remove accessors if
you throw some curly braces into the mix. Why does this matter? Imagine that you
have a MainForm, and a usercontrol named ControlPanel. ControlPanel
contains another usercontrol called hiddenControl that exposes an event that you
want to handle in MainForm, but all MainForm has access to is
ControlPanel...

```csharp
public event EventHandler<MyEventArgs> MyEvent{
	add{
		this.hiddenControl.MyEvent += value;
	}
	remove{
		this.hiddenControl.MyEvent -= value;
	}
}
```

Now you can subscribe to the event in MainForm without making the usercontrol
member public in ControlPanel.

[ Currently Playing : Burn Away - Foo Fighters - One by One
(4:57) ]
