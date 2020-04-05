---
layout: post
title: What to do if your Windows 2008 install won't activate complaining about no KMS server
date: 2009-12-29 11:09
author: chrispelatari
comments: true
categories: [professional_geek]
---

<p>Basically this is what happened:<br /><br />The MSDN subscriptions version of 
Windows Server 2008 installs by default using KMS (Key Management 
Service).<br />The key MSDN gave is a MAK (Multiple Activation Key).<br />So the 
install does not use the key, it tries to talk to KMS.<br />We don't have KMS here 
so it fails.<br /><br />Doing the following activates it using the MAK 
key:<br /><br />1) Open a cmd shell as Administrator.<br />2) Type the following (but 
use your key instead of all the X's)<br /><br />slmgr -ipk 
XXXXX-XXXXX-XXXXX-XXXXX-XXXXX<br /><br />3) The prompt will return right away, but 
there is a licensing task that it started (if you look in Task Manager you can 
find a task SLsvc using up cpu, I assume this is where the licensing is going 
on).<br />4) After a while a dialog will pop up saying that it has been 
activated.<br /><br />Good Luck</p>
<p>above was lifted from a forum post. buried in there is the command line to 
bypass KMS and use the proper MAK instead. It worked!</p>
<p>In the process of figuring this out, MSFT had me download a video explaining 
how to setup a KMS, one of the requirements is that you need 5 servers to 
contact KMS before it will work. That's fucking retarded. If I'm paying for a 
product, I expect that I'm paying for <strong>ease of use.</strong> Making your 
paying customers bend over backwards to use the product you are selling is 
unsustainable, bad business. You can do better than that, 
Microsoft.</p>
