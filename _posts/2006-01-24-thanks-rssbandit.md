---
layout: post
title: Thanks, RssBandit.
date: 2006-01-24 08:21
author: chrispelatari
comments: true
categories: [rssbandit,postxing]
---

[RssBandit](http://rssbandit.org) has been a big inspiration for
some of the specific features of [PostXING](http://postxing.net). As
a matter of fact, where possible I've used code from RssBandit directly. At
least half of proxy support, most of the plugin loading logic, and most recently
(like you don't have it unless you monitor the branches for postxing) a
little-used, very useful interface: IMessageFilter.
IMessageFilter is only implemented by the splitter control in the framework
(according to reflector) but was extremely helpful in the quest to better handle
the keyboard. There is only one method defined on the interface:

```csharp
//CF: thanks, rssbandit :)
public bool PreFilterMessage(ref Message m) {
  ...
}
```

The code then looks for the WM_KEYDOWN or WM_SYSKEYDOWN messages and handles
things according to whatever rules you put in there. To get it hooked up, I
simply overrode OnActivate and OnDeactivate and added
Application.Add/RemoveMessageFilter(this);

I figured if I already posted the problem, I might as well post a solution as
well. This was really helpful to the flat spot that was forming on my forehead,
so thanks again RssBandit.
