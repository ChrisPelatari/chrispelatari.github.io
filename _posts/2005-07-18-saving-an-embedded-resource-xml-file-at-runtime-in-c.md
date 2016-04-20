---
layout: post
title: Saving an embedded resource xml file at runtime in C#
date: 2005-07-18 19:37
author: chrispelatari
comments: true
categories: [Uncategorized]
---

<p>I couldn't find a cut &amp; dry solution to this (probably b/c it's too 
simple for anyone to think they would need an example) so here's how I got an 
xml file embedded as a resource in a vs2003 project written to the 
filesystem.</p>
<p>First, you just add an xml file with some default information you want for it 
to your project and change its build action to Embedded Resource. Then, you find 
the name of the resource (it can be tricky if you have a few folders) by opening 
up ildasm and double clicking the MANIFEST node. Using that resource name, you 
would do something like this:</p><pre><span style="color:blue;">using</span> System;
<span style="color:blue;">using</span> System.IO;
<span style="color:blue;">using</span> System.Xml;
<span style="color:blue;">using</span> System.Reflection;

<span style="color:blue;">string</span> path = Path.Combine(
Environment.GetFolderPath(
Environment.SpecialFolder.ApplicationData), 
Application.CompanyName);

path = Path.Combine(path, Application.ProductName);
path = Path.Combine(path, subFolder);
path = Path.Combine(path, <span style="color:maroon;">"fileName.xml"</span>);

<span style="color:blue;">if</span>(!File.Exists(path)){
	Assembly thisAssembly = Assembly.GetExecutingAssembly();
	Stream rgbxml = thisAssembly.GetManifestResourceStream(
<span style="color:maroon;">"YourNamespace.fileName.xml"</span>);			
	XmlDocument doc = <span style="color:blue;">new</span> XmlDocument();
	doc.Load(rgbxml);

	doc.PreserveWhitespace = <span style="color:maroon;">true</span>;
	doc.Save(path);					
}</pre>
<p>A couple of things to note about this: it's for a WinForms application, so I 
can use the Application class to get things in AssemblyInfo.cs (like 
ProductName, CompanyName). Also, you could probably do this anywhere but I chose 
to put a lot of my default configuration under the user's ApplicationData 
folder, where most users (can't say for sure about the guest account since 
that's been disabled here for a long time) have authority to 
write.</p>
