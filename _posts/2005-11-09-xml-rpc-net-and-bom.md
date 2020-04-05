---
layout: post
title: xml-rpc.net and BOM
date: 2005-11-09 08:13
author: chrispelatari
comments: true
categories: [professional_geek]
---

<p>I'm using <a href="http://xml-rpc.net">xml-rpc.net</a> as the library 
that supports xml-rpc for the MetaWeblog api in <a href="http://PostXING.url123.com/main">PostXING</a>.</p>
<p>I recently ran into a service endpoint that included a <a href="http://en.wikipedia.org/wiki/Byte_Order_Mark">Byte Order Mark</a> in 
the payload of the response. Something I haven't run into yet basically because 
the few blog engines that I have tested px with have not included this. It turns 
out that the XmlDocument.Load method that accepts a stream doesn't take this 
into account (or something:).</p>
<p>So this is what I did to workaround the problem: basically, if the first 
character is not &lt;, the second must be otherwise the content is invalid 
anyways.</p><pre><span style="color:green;">//...the DeserializeResponse method that accepts a stream
</span>StreamReader sr = <span style="color:blue;">new</span> StreamReader(stm);

<span style="color:blue;">string</span> content = sr.ReadToEnd();

<span style="color:blue;">if</span>(content.Trim().Length &gt; 0 &amp;&amp; content[<span style="color:maroon;">0</span>] != <span style="color:maroon;">'&lt;'</span>){
	content = content.Substring(<span style="color:maroon;">1</span>);
}

StringReader str = <span style="color:blue;">new</span> StringReader(content);

<span style="color:blue;">try</span>{
	xdoc.Load(str);
}</pre>
<p>The other endpoints still work after this modification, so I guess it's 
okay.</p>
<p><font color="#ff0000">update</font>: there was an indexoutofrange exception 
just waiting to happen up there.</p>
