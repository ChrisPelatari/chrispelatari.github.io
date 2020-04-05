---
layout: post
title: NetVibe&#58; Listen for SSID change
date: 2006-03-20 22:07
author: chrispelatari
comments: true
categories: [professional_geek]
---

<p>I've updated the NetVibe source with a mildly useful update: listening for
changes in SSID as well as IP Addresses. The source is hosted at <a href="http://chrisfrazier.net:8080/NetVibe">http://chrisfrazier.net:8080/NetVibe</a> on
a subversion server.</p>
<p>I used <a href="http://www.furrygoat.com/2004/05/finding_your_cu.html">some
code that I found at the FurryGoat experience</a>, modified it a little bit, and
it seems that it's at least useful in detecting if an SSID ends with
something...for example, my WiFi at work has an SSID of VelocityDatabank, so I
created a rule to look for an SSID/IP Address that EndsWith Databank. This code
definitely needs improvement, but I have found it very useful, and now I don't
have to have different network segments specified at each of the different WiFi
spots I connect to.</p>
