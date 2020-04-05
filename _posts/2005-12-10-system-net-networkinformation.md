---
layout: post
title: System.Net.NetworkInformation
date: 2005-12-10 07:59
author: chrispelatari
comments: true
categories: [professional_geek]
---
This is pretty cool:
<pre>System.Net.NetworkInformation.NetworkChange.NetworkAddressChanged += 
<span style="color:blue;">new</span> System.Net.NetworkInformation.NetworkAddressChangedEventHandler
(NetworkChange_NetworkAddressChanged);</pre>
I have a laptop that everyday switches between my wireless home network and
my wired work domain. I was looking for a way to add scripting abilities to the
interface itself (i.e. when a network connects, run some script) when I stumbled
upon this jem.

So, I now have a little winforms app that sits in my tray (yet another one)
and doesn't do anything but run a script (that in turn modifies my hosts file)
and change its tray icon when I'm connected to different networks.

Here's what connected at home looks like: <a href="http://chrispelatari.files.wordpress.com/2005/12/connectedhome.png"><img class="alignnone size-full wp-image-1169" alt="connectedhome" src="http://chrispelatari.files.wordpress.com/2005/12/connectedhome.png" width="32" height="38" /></a>

It began as a quick'n'dirty POC, and I started to make it more generalized by
extracting the common elements to an object model and persisting/loading. Then I
stopped myself. I'll just let this one remain quick'n'dirty for now. Why?
Because it works. And it saves me from having to remember to execute those batch
scripts every time I come home and logon or go to work and logon.

nice.
