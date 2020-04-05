---
layout: post
title: Divelements SandDock 2.0
date: 2005-07-13 16:48
author: chrispelatari
comments: true
categories: [professional_geek]
---
<a href="http://divil.co.uk/net/controls/sanddock/">Was just released</a>. In
the newsletter, it said that you can use a DocumentContainer (tabs) outside of a
SandDockManager - simple tabbing with the same interface that is all over <a href="http://PostXING.url123.com/main">PostXING</a>. Sounds promising!

Well, the "document" tabs only render
at the top, and I need tabs at the bottom to keep the interface at least a
little similar to what it always has been. Plus, with the interface that I have
in PostXING, I just like the way the tabs look at the bottom better. So I have
two choices: keep the interface that is already in place (using the older (free)
version of Magic) or have tabs at the top, right? Nope.

I found a way to use the docking
windows (that show their tabs at the bottom) to get the effect that I
wanted.

First, I created a usercontrol
and added four docking windows (with tabs). Then I expanded the dock
control that holds the windows to be the same width as the usercontrol and
anchored to top | left | right. After that, I basically disabled all docking,
closing, and extra actions. At a pinch of graphics, and this is what I
get:

<a href="http://chrispelatari.files.wordpress.com/2005/07/testsanddocktabs.png"><img class="alignnone size-full wp-image-1200" alt="testsanddocktabs" src="http://chrispelatari.files.wordpress.com/2005/07/testsanddocktabs.png" width="593" height="467" /></a>

Nice, huh? Well, I thought it
was anyways :)
